## Caching

- 장고에서 제공하는 캐싱 기능이 있다. 
- method_decorator를 사용하여 CBV의 데코레이터로 사용한다. 
- cache_page, vary_on_cookie와 같은 데코레이터들과 함께 사용할 수 있다. 

### 공식문서 예시

```python
from django.utils.decorators import method_decorator
from django.views.decorators.cache import cache_page
from django.views.decorators.vary import vary_on_cookie

from rest_framework.response import Response
from rest_framework.views import APIView
from rest_framework import viewsets


class UserViewSet(viewsets.ViewSet):

    # Cache requested url for each user for 2 hours
    @method_decorator(cache_page(60*60*2))
    @method_decorator(vary_on_cookie)
    def list(self, request, format=None):
        content = {
            'user_feed': request.user.get_user_feed()
        }
        return Response(content)


class PostView(APIView):

    # Cache page for the requested url
    @method_decorator(cache_page(60*60*2))
    def get(self, request, format=None):
        content = {
            'title': 'Post title',
            'body': 'Post content'
        }
        return Response(content)
```

