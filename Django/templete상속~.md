# Templete상속

templete 상속: 

  {% extends 'base.html' %}



  {% block content %}



~

 {% endblock %}



base.html

```
<div class="container">
{% block content %}
{% endblock %}
```



url 관리:

path('blog/',include('blog.urls'))



# Static

정적파일:

+ 미리 서버에 저장되어 있는 파일

+ 서버에 저장된 그대로를 서비스해주는 파일

동적파일:

+ 서버의 데이터들이 어느정도 가공된다음 보여지는 파일(상황에 따라 달라질 수 있음)



static: 개발자가 서버를 개발할 때 미리 넣어놓은 정적파일(img, js, css)

media: 사용자가 업로드 할 수 있는 파일

STATICFILES_DIRS=[

  os.path.join(BASE_DIR,'blog','static')]

\#현재 static 파일들이 어디에 있는지



STATIC_ROOT = os.path.join(BASE_DIR,'static')

\#static 파일을 어디에 모을건지



python manage.py collectstatic

#  media

### settings.py

MEDIA_ROOT= os.path.join(BASE_DIR,'media')

\#이용자가 업로드한 파일을 모으는 곳

MEDIA_URL = '/media/'



#### url

from django.conf import settings

from django.conf.urls.static import static



\+ static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)



#### models.py

image= models.ImageField(upload_to="blog/" , blank=True, null= True)

(upload_to 는 업로드할 폴더를 지정 하는 것이다. settings.py에 MEDIA_URL로 지정해둔 media 폴더 안에 blog폴더를 만들어서 관리하겠다는 설정입니다.)



pip install pillow

python manage.py makemigrations

python manage.py migrate



### new.html

enctype="multipart/form-data"

<p>사진: <input type="file" name="image"></p>



### views.py

 {% if blog.image%}  

new_blog.image = request.FILES['image']

  {%end if %}



 # Form 

forms.py 를 이용

장고에서 제공해주는 form

form 태그의 그 form 

입력 공간

데이터베이스 형식에 맞게 



### form.py

from django import forms

from .models import Blog



class BlogForm(forms.ModelForm):

  class Meta:

​    model = Blog

​    fields=['title','writer','body','image']

​    

### views.py

from .forms import BlogForm



def new(request):

  form =BlogForm()

  return render(request, 'new.html',{'form':form})



def create(request):

  form=BlogForm(request.POST, request.FILES)

  if form.is_valid():

​    new_blog=form.save(commit=False)

​    new_blog.pub_datr= timezone.now()

​    new_blog.save()

​    return redirect('detail',new_blog.id)

  return redirect('home')





### new.html

  {{form.as_p}} //p태그



<table>
    {{form.as_table}}//table
</table>



# User 확장과 인증

+ 장고에서 제공해주는  user
  + class user 상속

+ 장고에서 제공해주는 auth
  + authentication 인증
  + authenticate : 요청된 정보와 패스워드가 맞는지 함수
  + login: 인증된 상태를 만들어주는 함수
  + logout: 인증된 유저가 인증을 풀어달라는 요청

### 실습 1

$ python manage.py startapp account

+ settings.py: INSTALLED_APPS=['account']



+ views.py: 

   from django.contrib.auth.forms import AuthenticationForm, UserCreationForm

  from django.contrib.auth import authenticate,login, logout

```
    if request.method =='POST':
        form=AuthenticationForm(request=request, data=request.POST)
        if form.is_valid():
            username=form.cleaned_data.get("username")
            password=form.cleaned_data.get("password")
            user = authenticate(request=request, username=username,password=password)
            if user is not None:
                login(request, user)

        return redirect("home")
    else:
        form = AuthenticationForm()
        return render(request,'login.html',{'form':form})
```

```
def logout_view(request):
    logout(request)
    return redirect("home")
```

+ urls.py(account)

  from django.urls import path

  from .views import *

  urlpatterns = [

    path('login/',login_view,name="login"),

    path('logout/',logout_view, name="logout"),

  ]

+ urls.py(lionproject)

    path('account/',include('account.urls')),



+ base.html

   <a class="nav-link" href="{%url 'login' %}">Login</a>



### 실습 2

view.py

``` 
from .forms import RegisterForm

def register_view(request):
    if request.method=="POST":
        form= RegisterForm(request.POST)
        if form.is_valid():
            user= form.save()
            login(request, user)
        return redirect("home")
    else:
        form = RegisterForm()
        return render(request,'signup.html',{'form':form})
```

urls.py

```
    path('register/', register_view, name="signup"),
```



signup.html

```{% extends 'base.html' %}
{% extends 'base.html' %}

{% block content %}
<h1>
sign up !
</h1>

<form action="{% url 'signup' %}" method="post">
    {%csrf_token%}
    {{form.as_p}}
    <button type="submit">submit</button>
</form>
{% endblock %}
```

  {% if user.is_authenticated %}: 인증된 사람한테만

  {% if not user.is_authenticated %}: 인증되지 않은 사람



models.py(account)

```
from django.db import models
from django.contrib.auth.models import AbstractUser
# Create your models here.

class CustomUser(AbstractUser):
    nickname = models.CharField(max_length=100)
    university= models.CharField(max_length=50)
    location = models.CharField(max_length=200)
```



settings.py

```
AUTH_USER_MODEL ='account.CustomUser'
```



$ py manage.py makemigrations

오류가 뜨면 admin  주석(urls.py, settings.py)

$ python manage.py migrate



forms.py

```
from django.contrib.auth.forms import UserCreationForm
from .models import CustomUser

class RegisterForm(UserCreationForm):
    class Meta:
        model= CustomUser
        fields=['username','password1', 'password2','nickname','location','university']
```



home.html

```
    안녕하세요{{user.location}}에 사는{{user.useruniversity}} 다니는 {{user.nickname}}님 안녕하세요
```



admin.py

```
from django.contrib import admin
from .models import CustomUser
# Register your models here.

admin.site.register(CustomUser)
```



# Pagination

user확장과 인증

<a href="?page=1">

페이지 관련 정보도 있음

/?page = paginator.어떤페이지

#### view.py

```
from django.core.paginator import Paginator

def home(request):
    paginator= Paginator(blogs,3)
    page=request.GET.get('page')
    blogs = paginator.get_page(page)
```

#### home.html

```
    {% if blogs.has_previous %}
    <a href="/?page=1">처음</a>
    <a href="/?page={{blogs.previous_page_number}}">이전</a>
    {% endif %}
    <span>{{blogs.number}}</span>
    <span>of</span>
    <span>{{blogs.paginator.num_pages}}</span>
    {% if blogs.has_next %}
    <a href="?page={{blogs.next_page_number}}">다음</a>
    <a href="?page={{blogs.paginator.num_pages}}">마지막</a>
    {% endif %}
```



# Queryset, Method

#### view.py

```
def home(request):
    blogs=Blog.objects.order_by('-pub_date')//가장 오래된 순으로 재배치
    paginator= Paginator(blogs,3)
    page=request.GET.get('page')
    blogs = paginator.get_page(page)
    return render(request, 'home.html',{'blogs':blogs})
```



#### view.py, home.html

```
def home(request):
    blogs=Blog.objects.order_by('-pub_date')//가장 오래된 순으로 재배치
    search = request.GET.get('search')
    if search=='true':
    	author = request.GET.get('writer')
    	blogs = Blog.objects.filter(writer=author).order_by('-pub_date')//필터링 기능 filter(포함)<->exclude(제외), order_by도 가능
    paginator= Paginator(blogs,3)
    page=request.GET.get('page')
    blogs = paginator.get_page(page)
    return render(request, 'home.html',{'blogs':blogs})
    
 <a href = "?search=true&writer={{user.nickname}}">내가 쓴 글</a>
```



