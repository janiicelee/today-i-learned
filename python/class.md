## Class
- 파이썬은 모든 것이 객체이다. 클래스도 객체이고, 객체 즉 인스턴스를 생성한다.
- class의 필드를 수정하면 이미 생성되 있던 instance도 포함해서 모든 instance들이 같이 수정된다. 이러한 class object를 만들어내는  또 다른 special object를 metaclass 라고 한다. 파이썬에서 디폴트 metaclass는 type이다.
- type은 메타클래스 그 자체이다. 그래서 int, str, float 그리고 사용자가 만든 클래스의 데이터타입이 'type'으로 출력된 것이다.
- metaclass는 위에서 본 type을 상속받아서 만들 수 있다.

```python
class MyMetaClass(type):
   def __init__(cls, name, bases, namespace):
       super(MyMetaClass, cls).__init__(name, bases, namespace)
       cls.meta_function = lambda self: print("Hello")
​
class MyClass(metaclass=MyMetaClass):
   pass
​
obj = MyClass()
obj.meta_function()
​
-------------------------------------
Hello
```

참조: https://insung151.tistory.com/8