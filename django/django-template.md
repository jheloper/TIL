# Django Template

장고의 템플릿은 사용자에게 보여지는 사용자 인터페이스를 담당한다. 기본 템플릿 엔진은 장고에서 지원하는 DTL(Django Template Language)을 사용하며, 다른 템플릿 엔진으로 바꿀 수 있다.

기본적으로 HTML 파일이다.

템플릿 파일의 위치는 일단 프로젝트 템플릿 파일이냐, 애플리케이션 템플릿 파일이냐에 따라 달라진다. 프로젝트 템플릿 파일은 settings.py에 TEMPLATE_DIRS로 지정한 경로이며, 애플리케이션 템플릿 파일의 경우 애플리케이션 디렉토리 하위의 `/templates/애플리케이션명/`이다.

## 내부 처리 과정
1. 템플릿 설정에 따라 Engine 객체 생성.
2. 템플릿 파일 로딩 및 Template 객체 생성.
3. 렌더링 실시, 최종 HTML 텍스트 파일 생성.

장고의 템플릿 문법은 몇 가지가 있다.

## 제네릭 뷰 기본 템플릿명
모델을 사용하는 제네릭 뷰들은 대부분 기본 템플릿명을 가지고 있다. 제네릭 뷰에서 template_name 속성을 지정하지 않으면 이 기본 템플릿명으로 템플릿 파일을 찾는다.
다음 예시는 bookmark 앱의 Site 모델을 사용하는 제네릭 뷰들에 대한 예시이다

| 제네릭 뷰 | 기본 템플릿명 |
|-----|-----|
| ListView | bookmark/site_list.html |
| DetailView | bookmark/site_detail.html |
| ArchiveIndexView | bookmark/site_archive.html |
| YearArchiveView | bookmark/site_archive_year.html |
| MonthArchiveView | bookmark/site_archive_month.html |
| WeekArchiveView | bookmark/site_archive_week.html |
| DayArchiveView | bookmark/site_archive_day.html |
| TodayArchiveView | bookmark/site_archive_day.html |
| DateDetailView | bookmark/site_detail.html |
| CreateView | bookmark/site_form.html |
| UpdateView | bookmark/site_form.html |
| DeleteView | bookmark/site_confirm_delete.html |


## 템플릿 태그
`{% %}`의 경우 이미 정해진 문법에 따라 사용하는 태그. 템플릿 태그.

### {% extends %}
템플릿 상속 태그.
```html
{% extends "base.html" %}
```

### {% include %}
다른 템플릿 파일을 불러와서 포함시킨다.
```html
{% include "test.html" %}
```

### {% static %}
정적 파일 경로(STATIC_URL)를 조합.
```html
{% load static %}
<img src="{% static "images/hello.jpg" %}" />
```
장고에서 제공하는 staticfiles 앱에서도 동일한 이름의 태그를 사용. URL을 만드는 방법이 다름. staticfiles 앱에서 제공하는 태그는 클라우드 서버나 CDN의 서버에 존재할 경우 사용하며, STATICFILES_STORAGE 설정에 지정된 외부 서버의 정적 파일을 인식할 수 있다. 물론 로컬에 존재하는 정적 파일도 인식하기 때문에, 다른 이유가 없다면 staticfiles 앱의 {% static %} 태그를 사용하는 것을 권장한다.
```html
{% load staticfiles %}
<img src="{% static "images/hello.jpg" %}" />
```

### {% for %}
```html
<ul>
{% for item in object_list %}
    <li>{{ item.name }}</li>
{% endfor %}
</ul>
```

### {% if %}
```html
{% if object_list %}
    {{ object_list }}
{% elif other_object_list %}
    {{ other_object_list }}
{% else %}
    "No List."
{% endif %}
```

### {% csrf_token %}
장고에서는 POST 전송의 폼을 사용하는 경우 CSRF(Cross Site Request Forgery) 공격을 방지하기 위해 이 태그를 사용해야 한다. 다만 외부 URL로 보내는 폼에는 사용하지 않도록 한다.
```html
<form action="." method="post">{% csrf_token %}
```

### {% url %}
```html
<form action="{% url 'blog:detail' post.id %}" method="post">
```

### {% with %}
특정 값을 범위 내에서 사용하기 위해 저장하는 기능을 한다. 유효 범위는 {% endwith %} 태그까지다.
```html
{% with number=example.item.count %}
    {{ number }} is example item count.
{% endwith %}
```

### {% load %}
장고에서 제공하는 태그 및 필터, 또는 사용자 정의 태그 및 필터를 사용할 수 있도록 로딩한다.
```html
{% load staticfiles %}
```

## 템플릿 변수
`{{ }}`의 경우 뷰에서 보낸 변수를 사용하는 태그. 템플릿 변수.
```html
<div>{{ example.number }}</div>
```
만약 정의되어 있지 않은 변수라면, 빈 문자열로 대체된다.


## 템플릿 필터
`{{ | }}`의 경우 템플릿 필터. 템플릿 변수에 필터를 적용하여 변수의 출력 결과를 변경하는 데에 사용. 자세한 사용법은 [장고 공식 문서 해당 내용](https://docs.djangoproject.com/en/1.10/ref/templates/builtins/) 참고할 것.


## 템플릿 주석
`{# #}` 템플릿 주석. 이 안에 들어간 내용은 렌더링되지 않는다.
```html
<div>{# this is comment #}Hello, world!</div>
```
