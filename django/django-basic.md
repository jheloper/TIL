# Django 기본 개념

# 개요
장고(Django)는 대표적인 파이썬 웹 프레임워크 중 하나.

MVC(Model View Controller) 패턴과 유사한 MTV(Model Template View) 패턴으로 구현되었다.


# 장고의 시작

## 환경 구성 및 관리자 기능 활성
당연히 설치부터 시작한다. 파이썬 패키지 매니저인 pip를 사용하면 쉽고 간편하다.
일단 파이썬 가상환경인 virtualenv를 이용하여 독립된 개발환경을 설정한다(virtualenv의 사용은 필수가 아니지만 모듈 및 패키지의 의존성 ).
```bash
mkdir django-test
cd django-test
virtualenv 가상환경이름
source 가상환경이름/bin/activate
```
이후 pip를 이용하여 장고를 설치한다(버전을 기입하지 않아도 된다. 버전을 기입하지 않으면 현재 pip에 올라온 최신 버전으로 설치된다).

`pip install django==버전`

이것으로 장고 설치는 끝났다. 그럼 이제 장고 프로젝트를 생성하도록 하자.

`django-admin startproject 프로젝트이름 .`

그럼 이제 해당 경로에 몇 가지의 파일과 디렉터리가 생성된다.
기본적인 관리자 사이트를 열어보자.
```bash
python manage.py createsuperuser
python manage.py migrate
python manage.py runserver
```
1번째 라인은 Super User 계정을 대화형으로 생성하고
2번째 라인은 DB를 생성하며
3번째 라인은 서버를 실행시킨다. 이제 우리는 웹 브라우저를 통해 `127.0.0.1:8000/admin` 으로 관리자 사이트에 접근할 수 있다.

## 애플리케이션 추가
장고는 프로젝트와 애플리케이션이라는 개념이 있는데, 자세한 것은 장고 공식 사이트의 문서를 참고하면 알 수 있다.
애플리케이션을 생성하려면 다음과 같이 하면 된다.

`python manage.py startapp 앱이름`

그럼 애플리케이션 디렉터리와 기본적인 파일이 생성된다.

## 애플리케이션 등록
장고의 애플리케이션은 생성만 해서는 의미가 없다. 프로젝트에 등록해줘야 한다.

settings.py 파일을 열어보면 **INSTALLED_APPS** 이라는 항목이 있으며, 여기에 앱 이름이 'bookmark'라면 `bookmark.apps.BookmarkConfig`라고 넣어주면 된다. 이것은 애플리케이션 설정 클래스이며, `django.apps.AppConfig`를 상속받는다.

## DB 변경사항 적용
DB에 무언가 변경사항이 생겼을 경우, 다음 명령어를 통해 적용시킨다.
```bash
python manage.py makemigraions
python manage.py migrate
```
만약 애플리케이션 DB의 적용이 정상적으로 이뤄지지 않을 경우 `python manage.py makemigrations 앱이름` 형식으로 명령어를 실행시킨다.

## 프로젝트 설정
settings.py는 프로젝트 전반에 대한 설정이 있는 파일이다. 여기서 몇 가지 중요한 설정들이 있다.

- 애플리케이션 등록은 INSTALLED_APPS 확인.
- 데이터베이스 관련 사항은 DATABASES 확인.
- 템플릿 관련 사항은 TEMPLATES 확인.
- 정적 파일(js, css 등) 관련 사항은 STATIC_URL, STATICFILES_DIRS 확인.
- 타임존은 TIME_ZONE 확인(대한민국은 'Asia/Seoul'로 바꿔주면 된다).
- 미디어(이미지 등) 관련 사항은 MEDIA_URL, MEDIA_ROOT 확인.
- 언어 관련 사항은 LANGUAGE_CODE 확인(한국어는 'ko-kr', 영어는 'en-us').

## 대략적인 개발 순서
다음 순서는 절대적인 기준이 아님을 명심할 것.

1. 장고 프로젝트를 생성한다.
2. 장고 애플리케이션을 생성한다.
3. settings.py에서 관련 설정을 지정한다.
4. URLconfig 설정
5. 모델 개발
6. 뷰 개발
7. 템플릿 개발
8. DB makemigrations & migrate
9. 서버를 실행하여 확인.
