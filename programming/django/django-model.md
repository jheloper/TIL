# Django Model

장고의 ORM(Object Relation Mapping) 기능을 이용하여 데이터베이스 관련 작업을 수행한다.

## 테이블 정의
```python
class User(models.Model):
    name = models.CharField(max_length=200)
    ......
```
모델 클래스가 즉 데이터베이스의 테이블이 되며, 모델 클래스의 멤버가 테이블의 컬럼이 된다.

모델 클래스는 `django.db.models.Model` 클래스를 상속받아서 정의하고, 모델 클래스의 멤버도 장고에서 미리 정의해 둔 모델 필드 클래스를 사용하여 정의한다.

정의한 모델 클래스를 관리자 페이지에서 확인하기 위해서는 admin.py에 `admin.site.register()` 함수를 사용한다.

## 필드
### CharField
```python
class User(models.Model):
    name = models.CharField(max_length=200)
```
문자열을 표현하기 위한 필드. `max_length` 속성 지정이 반드시 필요하다. 기본 위젯은 Test Input이다.

### TextField
```python
class User(models.Model):
    description = models.TextField()
```
많은 양의 문자열을 표현하기 위한 필드. `max_length` 지정이 필요하지 않다. 기본 위젯은 Text Area이다.

### DateTimeField
```python
class User(models.Model):
    register_date = models.DateTimeField()
```
일시를 표현하기 위한 필드. 파이썬의 `datetime.datetime`을 사용한다. 날짜를 표현하기 위해서는 `models.DateField`를, 시간을 표현하기 위해서는 `models.TimeField`를 사용한다. `auto_now` 및 `auto_now_add` 속성 등을 지정할 수 있다.

auto_now : 저장될 때 현재 일시를 자동으로 설정. *수정일시*로 자주 쓰인다.

auto_now_add : 생성될 때 현재 일시를 자동으로 설정. *생성일시*로 자주 쓰인다.

### IntegerField
```python
class User(models.Model):
    consumer_number = models.IntegerField()
```
Integer 값을 표현하기 위한 필드. 64비트 Integer 값을 사용하려면 `models.BigIntegerField`를 사용하면 된다.

### BooleanField
```python
class User(models.Model):
    is_admin = models.BooleanField()
```
True, False. Null은 허용하지 않으며 `models.NullBooleanField`을 사용하면 Boolean 값과 함께 Null 값도 사용할 수 있다. 기본 위젯은 Check Box.

### DecimalField
```python
class User(models.Model):
    score = models.DecimalField(max_digits=5, decimal_places=2)
```
고정 소수점 10진수를 표현하기 위한 필드.

max_digits, decimal_places 속성이 반드시 지정되어야 한다.

max_digits : 최대 자릿수

decimal_places : 소수 자릿수

### FileField
```python
class Article(models.Model):
    attachment_file = models.FileField(upload_to='uploads/%Y/%m/%d')
```
파일 업로드 필드. `upload_to` 속성을 통해 파일이 저장될 경로를 지정할 수 있다. 기본적으로는 settings.py에 지정된 MEDIA_ROOT 경로에 upload_to로 지정한 경로를 합쳐서 해당 경로에 파일을 저장한다. 이미지 파일을 업로드할 때에는 `models.ImageField`를 사용하면 된다.

## 필드 옵션
- null : 기본값은 False.
- blank : 기본값은 False.
- primary_key : 해당 필드를 모델의 PK(Primary Key)로 지정한다.
- unique : 해당 필드를 유니크 속성으로 지정한다.
- default : 해당 필드의 기본값을 지정한다.
- db_column : 해당 필드의 데이터베이스 컬럼명을 지정한다.

## Model Manager
장고의 모델 클래스는 기본적으로 매니저를 가져야 한다. 모델을 정의할 때 명시적으로 지정하지 않으면 매니저의 기본 이름은 **objects**가 된다. 모델 매니저는 인스턴스 멤버가 아닌 **클래스 멤버**이다.

모델 매니저를 통해서 데이터베이스 쿼리가 사용되며, 쿼리셋 객체를 반환한다.

all(), filter(), exclude(), get(), count() 등의 메서드를 사용할 수 있다.
