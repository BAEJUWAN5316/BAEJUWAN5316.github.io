# 장고 세팅


- 가상환경 만들기
```python
# 터미널
python -m venv venv
```
지정 폴더 내 가상환경 폴더가 생성된다.

- 가상환경 안으로 들어가기
```python
# 터미널
.\venv\Scripts\activate
```

- 자동 가상환경 접속 만들기
보기 > 명령 팔레트 > select interpreter 누르기
```python
# 터미널
.\venv\Scripts\activate
```
위 두 번 누르면 완료

- 장고 설치하기
```python
# 터미널
python -m pip install "django~=5.2.0"
```
5.2.0번대 장고가 설치된다

- 장고 실행하기
```python
# 터미널
python -m django startproject config .
```
장고가 실행되고 자동으로 config 폴더랑 manage.py파일이 생성된다.

- 장고에서 사용 가능한 명령어 확인하기
```python
# 터미널
python manage.py --help
```
장고 터미널에서 실행 가능한 명령어들을 확인할 수 있다.

- 장고 서버 켜기
```python
# 터미널
python manage.py runserver
```
장고 서버가 켜지고 로컬호스트에 접속 가능해진다.

- 장고 데이터베이스 세팅하기
```python
# 터미널
python manage.py migrate
```
db.sqlite3 파일의 데이터베이스 테이블을 기본으로 자동세팅해준다.

- 관리자 계정 만들기
```python
# 터미널
python manage.py createsuperuser
```
admin 페이지에서 사용할 수 있는 계정을 만들어 준다
유저id, pw등을 설정하자

- 앱 만들기 (예시: chat)
```python
# 터미널
python manage.py startapp chat
```
'chat'이라는 앱(프로그램) 폴더가 생성되며 내부에 기본으로 파일과 폴더가 세팅된다.

- chat앱 폴더 장고와 연동시키기
```python
# config/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'chat', #add
]
```
config/settings.py에 들어가서
30번째쯤에 있는 [INSTALLED_APPS]리스트 안에
'chat'을 추가시켜주자
> 앱 chat폴더가 메인 장고와 연동 완료

- 앱 chat의 url(엔드포인트) 연동시키기
```python
# config.urls.py
from django.contrib import admin
from django.urls import path, include #add

urlpatterns = [
    path('admin/', admin.site.urls),
    path('chat/', include('chat.urls')) #add
]
```
config/urls.py 파일에 들어가기
[from django.urls import path] 여기뒤에 include 추가해서
[from django.urls import path, include] 이렇게 만들어주고,
그리고 admin 밑에 urlpatterns 리스트 안에
path('chat/', include('chat.urls'))넣어주기
> chat/urls.py에서 만들어주는 엔드포인트는 모두 chat/으로 시작한다는 뜻!

- 사용자에게 보여줄 html 파일 생성과 장고서버를 연결시켜주기
앱 폴더인 [chat]에 커서를 클릭하고 새파일 생성을 누른다.
[templates/chat/index.html] 이라고 써서 새 파일을 만들어준다.
```python
# chat.views.py
from django.http import HttpRequest, HttpResponse # add
from django.shortcuts import render

def index(request: HttpRequest) -> HttpResponse: # add
    return render(request,
      "chat/index.html" # 보이게 해줄 html파일 이름
      )
```
chat.views.py파일에 들어가서 제일 상단에
[from django.http import HttpRequest, HttpResponse] 이거를 추가해주자
그리고 위와같이 함수를 작성하면 [index]라는 함수 이름으로 index.html파일이 연결된다.

- html파일의 엔드포인트 지정하기
chat/urls.py 라는 파일을 만들어준다.
```python
#chat/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path("", views.index),
]
```
해당 파일 안에 위와 같이 작성해준다.
""이건 빈 엔드포인트, 즉 기본 엔드포인트인 [/chat]으로 보여주겠다는 뜻이다.
만약 "hello/"라고 쓴다면 [/chat/hello/] 의 엔드포인트로 접속가능해진다.
views. 뒤에 views.py에서 지정해준 함수의 이름을 써주면 연결 완료된다.
