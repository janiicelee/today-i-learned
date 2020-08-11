## How to delete cache function

- 장고 기본의 cache_page 장식자는 GET/HEAD 요청에 대해서 캐싱 로직을 동작시키며, 그 이외의 요청 (POST, PUT 등) 에 대해서는 특별한 처리를 하지 않습니다.

- cache_page 장식자는 timeout 이 지난 후에 expire 되며, expire time 전에 캐싱을 삭제할려면 low level cache api로 cache key 문자열을 직접 조합하여 삭제하여야만 합니다.

- cache_page 장식자는 내부적으로 CacheMiddleware를 사용하며, CacheMiddleware에 주요 로직들이 구현되어있습니다. 다음과 같이 CacheMiddleware를 상속받아 POST 요청 시에 관련 캐시를 삭제토록 구현해볼 수 있습니다.


- decorator.py
```python
from django.middleware.cache import CacheMiddleware
from django.utils.cache import get_cache_key
from django.utils.decorators import decorator_from_middleware_with_args


class PostDeleterCacheMiddleware(CacheMiddleware):
    def process_request(self, request):
        if request.method == 'POST':
            # https://github.com/django/django/blob/3.0.9/django/middleware/cache.py#L137
            cache_key = get_cache_key(request, self.key_prefix, 'GET', cache=self.cache)
            self.cache.delete(cache_key)
        return super().process_request(request)


def post_deleter_cache_page(timeout, *, cache=None, key_prefix=None):
    return decorator_from_middleware_with_args(PostDeleterCacheMiddleware)(
        page_timeout=timeout, cache_alias=cache, key_prefix=key_prefix,
    )
```

- views.py
```python
import datetime
from django.http import HttpResponse
from django.views.decorators.csrf import csrf_exempt
from .decorators import post_deleter_cache_page


@csrf_exempt
@post_deleter_cache_page(60)
def index(request):
    return HttpResponse(f"Hello World : {datetime.datetime.now()}")
```

## 특정 key_prefix 이용하여 삭제하기
```
cache.delete_pattern('*' + 'key_prefix' + '*')
```
- cache할때 key_prefix 먼저 설정하고 이후에 cache의 메소드인 delete pattern 활용하기 