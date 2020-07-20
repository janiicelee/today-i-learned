## Pagination
페이지네이션은 크게 두가지 방법이 있음.
두 방법 모두 url의 get parameter를 이용하여 이를 지원해준다.

1. PageNumberPagination ( page : 몉번째 페이지인지 표시. 페이지는 1부터 시작. / page_size: 한 페이지에 몇개의 레코드를 보여줄지 표시)
2. LimitOffsetPagination ( offset: 몇번째 레코드부터 보여줄지 설정해준다. 설정하지 않을시 첫번쨰 레코드부터 보여준다/ limit: 몇개의 레코드를 보여줄지 설정한다. / offset번째 레코드부터 offset+limit-1 번째 레코드까지 보여준다)

### custom pagination styles
- django project에서 각 레파지토리에 pagination.py를 만들고 해당 api 에 맞게 커스터마이징해야한다. 
- 공식문서 예시
```python
class CustomPagination(pagination.PageNumberPagination):
    def get_paginated_response(self, data):
        return Response({
            'links': {
                'next': self.get_next_link(),
                'previous': self.get_previous_link()
            },
            'count': self.page.paginator.count,
            'results': data
        })
```
### page size 전역변수로 설정 후 가져와서 쓰기
- settings   
```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.LimitOffsetPagination',
    'PAGE_SIZE': 100
}
```
- views   
```python
from rest_framework.pagination import PageNumberPagination

class ListPagination(PageNumberPagination):
    
    page_size_query_param = 'page_size'
    ...
```

