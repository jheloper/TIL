# Django View

## 함수형 뷰와 클래스형 뷰
함수형 뷰는 구현이 간단하지만, 클래스형 뷰가 더 많은 장점을 가진다. 상속과 믹스인을 사용하여 코드를 재사용할 수 있으며 체계적인 구성에 적합하고 장고에서 지원하는 제네릭 뷰(Generic View)를 사용할 수 있다.

클래스형 뷰의 경우, URLconf에서 `as_view()` 메서드를 통해 뷰에 진입한다. as_view() 메서드는 내부적으로 클래스형 뷰의 인스턴스를 생성하고, `dispatch()` 메서드를 호출하여 요청의 HTTP 메서드에 따라 해당 요청 메서드로 중계하는 역할을 한다. 만약 해당 요청 메서드가 정의되어 있지 않으면 `HttpResponseNotAllowed Exception`이 발생.

## 클래스형 뷰의 장점
- HTTP 요청 메서드에 따른 처리 코드를 조건문을 사용하지 않고 메서드명으로 구분할 수 있음.
- 제네릭 뷰 및 믹스인(Mix-in)을 사용할 수 있음.

## 제네릭 뷰
| 분류 | 이름 | 기능 |
-----|-----|-----
| Base | View         | 제네릭 뷰의 기본이 되는 최상위 제네릭 뷰.
|      | TemplateView | 템플릿을 렌더링하는 뷰.
|      | RedirectView | 해당 URL로 리다이렉트하는 뷰.
| Display | DetailView | 하나의 객체에 대한 상세 정보 뷰.
|         | ListView   | 객체의 리스트를 보여주는 뷰.
| Edit | FormView   | 폼을 렌더링하는 뷰.
|      | CreateView | 객체 생성 폼을 렌더링하는 뷰.
|      | UpdateView | 객체 수정 폼을 렌더링하는 뷰.
|      | DeleteView | 객체 삭제 폼을 렌더링하는 뷰.
| Date | YearArchiveView  | 주어지는 연도에 해당하는 객체를 보여주는 뷰.
|      | MonthArchiveView | 주어지는 연월에 해당하는 객체를 보여주는 뷰.
|      | WeekArchiveView  | 주어지는 연도, 주차에 해당하는 객체를 보여주는 뷰.
|      | DayArchiveView   | 주어지는 날짜에 해당하는 객체를 보여주는 뷰.
|      | TodayArchiveView | 오늘 날짜에 해당하는 객체를 보여쥬는 뷰.
|      | DateDetailView   | 연, 월, 일, 기본키에 해당하는 특정 객체 하나의 상세 정보를 보여주는 뷰.

## 제네릭 뷰 설명
### View
최상위 제네릭 뷰. 모든 클래스형 뷰는 이 클래스를 상속받는다. 적절한 제네릭 뷰가 없을 경우 직접 이 클래스를 상속하여 클래스형 뷰를 구현할 수 있다.
```python
class ExampleView(View):
    def get(self, request, *args, **kwargs):
        return HttpResponse('Hello, World!')
```

### TemplateView
템플릿 파일을 렌더링하는 뷰. 템플릿 파일명을 template_name 속성에 지정해주면 해당 파일을 렌더링하여 보여준다.
```python
class ExampleView(TemplateView):
    template_name = 'index.html'
```

### RedirectView
주어진 URL로 리다이렉트하는 뷰. url 속성에 리다이렉트할 URL을 반드시 지정해줘야 한다. URL 대신 URL 패턴명을 지정해도 된다.
```python
class ExampleView(RedirectView):
    url = '/blog/index/'
```

### DetailView
특정 레코드 하나의 상세정보를 보여주는 뷰. 레코드를 `object` 컨텍스트 변수에 담아 템플릿으로 보내준다.
```python
class ExampleView(DetailView):
    model = User
```
특정 객체 하나를 식별하기 위해 필요한 파라미터는 URLconf에서 넘겨주도록 지정한다.
```python
url(r'^post/(?P<slug>[-\w]+)/$', ,name='')
```

### ListView
레코드 리스트를 보여주는 뷰. 레코드 리스트를 `object_list` 컨텍스트 변수에 담아 템플릿으로 보내준다.
```python
class ExampleView(ListView):
    model = Post
```

### FormView
폼을 보여주기 위한 제네릭 뷰. form_class, template_name, success_url 속성이 주요 속성.
```python
class ExampleView(FormView):
    form_class = ExampleForm
    template_name = 'form.html'

    def form_valid(self, form):
        data = self.request.POST['data']
        Post.objects.filter()

        context = {}
        context['form'] = form
        context['data'] = data
        context['post_list'] = post_list

        return render(self.request, self.template_name, context)
```

### CreateView
새로운 레코드를 생성하기 위한 제네릭 뷰. 레코드 정보를 입력받을 수 있는 폼을 자동으로 만들어주며 폼에 입력된 정보를 데이터베이스에 저장하는 기능을 포함. model, fields, success_url이 주요 속성. 기본 템플릿 파일명은 '모델명소문자_form.html'.
```python
class ExampleView(CreateView):
    model = Post
    fields = ['title', 'description', 'content']
    initial = {}
    success_url = reverse_lazy('post:index')

    def form_valid(self, form):
        form.instance.owner = self.request.User
        return super(ExampleView, self).form_valid(form)
```

### UpdateView
이미 존재하는 레코드를 수정하기 위한 제네릭 뷰. CreateView와 유사하며, 다만 기능의 차이를 유의할 것.
```python
class ExampleView(UpdateView):
    model = Post
    fields = ['title', 'description', 'content']
    success_url = reverse_lazy('post:index')
```

### DeleteView
기존 레코드를 삭제하기 위한 제네릭 뷰. 삭제 처리는 내부에서 이뤄지고 코드에 나타나는 것은 삭제확인 화면. DeleteView는 CreateView나 UpdateView와 달리 데이터 입력 폼이 존재하지 않고 삭제 확인용 폼만 있으며, 따라서 model, success_url 속성이 주요 속성이다.
```python
class ExampleView(DeleteView):
    model = Post
    success_url = reverse_lazy('post:index')
```

### 날짜 기반 뷰 내용은 추후 추가 예정...

## 제네릭 뷰 속성 오버라이딩
### model
기본 뷰 3개(View, TemplateView, RedirectView)를 제외한 모든 제네릭 뷰에서 사용하는 속성. 뷰가 출력할 데이터가 들어 있는 모델을 지정. model 대신 queryset 속성으로 지정할 수도 있음. 밑의 두 가지 표현은 동일한 의미다.
```python
model = Post
queryset = Post.objects.all()
```

### queryset
기본 뷰 3개를 제외한 모든 제네릭 뷰에서 사용. 출력 대상이 되는 `QuerySet` 객체 지정. queryset 속성을 지정하면 model 속성은 무시된다.

### template_name
모든 제네릭 뷰에서 사용하는 속성. 템플릿 파일명은 문자열로 지정한다.

### context_object_name
기본 뷰 3개를 제외한 모든 제네릭 뷰에서 사용. 템플릿 파일에서 사용할 컨텍스트 변수명을 지정한다.

### paginate_by
ListView와 날짜 기반 뷰에서 사용. 페이징 기능이 활성화된 경우에 페이지당 몇 개 항목을 출력할지 정수로 지정한다.

### date_field
날짜 기반 뷰에서 사용. 기준이 되는 필드를 지정한다. 이 필드를 기준으로 연/월/일을 검사한다. 이 필드 타입은 `DateField`, 또는 `DateTimeField`이어야 한다.

### make_object_list
YearArchiveView에서 해당 연도에 맞는 객체들의 리스트를 생성할지 여부를 지정. True리면 객체들의 리스트를 만들고 그 리스트를 템플릿에서 사용 가능. False이면 queryset 속성에 None 할당.

### form_class
FormView, CreateView, UpdateView에서 사용하는 속성. 폼을 만드는 데 사용할 클래스를 지정.

### initial
FormView, CreateView, UpdateView에서 사용하는 속성. 폼에 사용할 초기 데이터를 딕셔너리로 지정.

### fields
CreateView, UpdateView에서 사용. 폼에 사용할 필드를 지정. `ModelForm` 클래스의 내부 클래스 `Meta.fields` 속성과 동일한 기능.

### success_url
FormView, CreateView, UpdateView, DeleteView에서 사용. 폼에 대한 처리가 성공한 후 리다이렉트할 URL 지정.

## 제네릭 뷰 메서드 오버라이딩
### get_queryset()
기본 뷰 3개를 제외한 모든 제네릭 뷰에서 사용하는 메서드. 출력 객체를 검색하기 위한 대상 QuerySet 객체 또는 출력 대상인 객체 리스트 반환. 기본은 queryset 속성값을 반환하지만, queryset이 지정되지 않은 경우 모델 매니저 클래스의 `all()` 메서드를 호출하여 쿼리셋 객체를 생성해 반환한다.

### get_context_data(**kwargs)
모든 제네릭 뷰에서 사용하는 메서드. 템플릿에서 사용할 컨텍스트 데이터를 반환한다.

### form_valid(form)
FormView, CreateView, UpdateView에서 사용하는 메서드. `get_success_url()` 메서드가 반환하는 URL로 리다이렉트 수행.


## 단축(Shortcut) 함수
### render_to_response()
```python
render_to_response(template_name, context=None, context_instance=_context_instance_undefined, content_type=None, status=None, dirs=_dirs_undefined, using=None)
```
템플릿 파일과 컨텍스트 데이터를 파라미터로 받아서 렌더링 처리 후, `HttpResponse` 객체를 반환하는 함수. template_name은 필수 파라미터이며, 나머지 인자들은 모두 선택 파라미터이다.

### render()
```python
render(request, template_name, context=None, context_instance=_context_instance_undefined, content_type=None, status=None, current_app=_current_app_undefined, dirs=_dirs_undefined, using=None)
```
render_to_response() 함수와 비슷한 기능을 하지만, request 파라미터를 필수로 받는다는 점이 다르다. 왜냐하면 `Context` 객체가 아닌 `RequestContext` 객체를 사용해 렌더링 처리하기 때문. request 및 template_name 파라미터는 필수이며, 나머지 파라미터는 선택 파라미터이다.

### redirect()
```python
redirect(to, permanenet=False, *args, **kwargs)
```
to 파라미터로 주어진 URL로 이동하기 위한 `HttpResponseRedirect` 객체를 반환. to 파라미터는 이동하기 위한 URL을 직접 지정하거나, 모델명을 지정하여 모델의 `get_absolute_url()` 메서드에서 반환하는 URL을 사용하거나, 뷰 이름을 지정하여 reverse() 함수를 해당 뷰 이름으로 파라미터를 넘겨주고 결과로 반환되는 URL을 사용할 수 있다.

### get_object_or_404()
```python
get_object_or_404(klass, *args, **kwargs)
```
klass 파라미터에 해당하는 모델에서 나머지 파라미터로 주어진 조건에 맞는 레코드 검색. 있으면 해당 레코드를 반환하고 없으면 `Http404 Exception`을 발생시킨다. 조건에 맞는 레코드가 여러 개일 경우에도 `MultipleObjectsReturned Exception`을 발생시킨다. klass 파라미터로는 모델이나 모델 매니저 클래스, 또는 쿼리셋 객체를 넣을 수 있다.

### get_list_or_404()
```python
get_list_or_404(klass, *args, **kwargs)
```
klass 파라미터에 해당하는 모델에서 나머지 파라미터로 주어진 조건에 맞는 레코드들을 검색. `get_object_or_404()` 함수와 다른 것은 리스트를 반환한다는 것이다. klass 파라미터로는 모델이나 모델 매니저 클래스, 또는 쿼리셋 객체를 넣을 수 있으며, 모델 매니저 클래스의 `filter()` 메서드를 사용해 검색한다.
