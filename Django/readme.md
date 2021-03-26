# Django, DjangoRestFramework

- 우선 프로젝트 폴더로 가서 아래 명령어를 입력하여 어드민 페이지를 활성화하자.  
  프로젝트 명은 `MyProject`라 한다.

```
django-admin startproject MyProject
```

- 이후 생성된 `MyProject` 폴더로 가서 아래 명령어를 입력하자.

```
python manage.py migrate
```

- 위 명령어가 생성된 후, 아래 명령어를 통해 서버를 실행해보자.

```
python manage.py runserver
```

- 위에서는 `MyProject`라는 Django Project를 생성했고, 이제 새로운 application을 생성해보자.  
  application명은 `api_basic`라 해보자.

```
python manage.py startapp api_basic
```

- 마지막으로 어드민 페이지에서 사용할 Super user를 아래 명령어를 통해 생성하자.

```
python manage.py createsuperuser
```

<hr/>

# Serializer

<h3>Article Model 생성</h3>

- 우선 위에서 `api_basic`이라는 애플리케이션을 생성하면 `api_basic`폴더 하위에  
  `models.py`라는 파일이 생성된다.

- `Serializer`는 요청에 대한 응답을 JSON 형식으로 변환해주는 기능을 제공하는 일종의 변환기이다.  
  우선, 예시로 `Article`라는 테이블이 있다고 하고, 이를 파이썬 코드로 표현해보자.

```py
# models.py

class Article(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=100)
    email = models.EmailField(max_length=100)

    def __str__(self):
        return self.title
```

- 위에서 작성하는 `__str__` 함수는 어드민 페이지에서 테이블의 데이터로 출력되는 값을 의미한다.

* 다음으로, `MyProject` 폴더 하위에 있는 `settings.py`의 `INTALLED_APPS`에 아래 2개를 추가해주자.

```py
# settings.py

# 다른 설정들
# Application definition

INSTALLED_APPS = [
    # 기존의 값들
    'rest_framework',
    'api_basic'
]
```

- 이제 이렇게 생성된 모델이 실제 테이블에 들어가게 하기 위해 migration을 진행해야 한다.  
  `MyProject` 폴더로 이동 후 아래 명령어를 입력하자.

```
python manage.py makemigrations

python manage.py migrtate
```

- 마지막으로 어드민 페이지에서 Article에 대한 정보를 볼 수 있도록 `admin.py`에 아래를 추가해주자.

```py
# admin.py

from django.contrib import admin
from .models import Article

admin.site.register(Article)
```

- 이제 어드민 페이지 (`http://localhost:8000/admin`)에 가면 Article을 볼 수 있다.

<h3>Article Serializer 작성</h3>

- Article을 JSON으로 변환해줄 Serializer를 작성해보자.  
  이 파일은 `api_basic`폴더 하위에 `serializers.py`로 하자.

```py
from rest_framework import serializers
from .models import Article

class ArticleSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=100)
    author = serializers.CharField(max_length=100)
    email = serializers.EmailField(max_length=100)

    def create(self, validated_data):
        return Article.objects.create(validated_data)

    def update(self, instance, validated_data):
        instance.title = validated_data.get('title', instance.title)
        instance.author = validated_data.get('author', instance.author)
        instance.email = validated_data.get('email', instance.email)
        instance.save() # 인스턴스를 save한다.
        return instance

```

- `serializers.Serializer`를 상속하는 클래스를 만들 때에는 JSON에 포함될 필드들을 선언해야 한다.  
  위에서는 title, author, email의 필드를 선언해주었다.
- `create()`와 `update()` 메소드는 우리가 원하는 필드들(title, author, email)이 포함된  
  데이터(validated_data)가 주어질 때 인스턴스를 저장하거나 UPDATE하는 메소드이다.

<h3>Testing ArticleSerializer</h3>

- 이제 위에서 작성한 `ArticleSerializer`를 테스트 해보자.  
  `python manage.py shell`로 파이썬 쉘에 들어온 후, 아래 코드를 입력 해보자.

```py
# Testing ArticleSerializer

from api_basic.models import Article
from api_basic.serializers import ArticleSerializer
from rest_framework.renderers import JSONRenderer
from rest_framework.parsers import JSONParser

# Article 객세 생성
article = Article(title = 'sample title', author = 'sample author', email = 'sample@sample.com')

# Article 객체를 DB에 저장
article.save()

# ArticleSerializer 객체 생성
serializer = new ArticleSerializer(article)

# JSON 형식으로 article 데이터 보기
serializer.data
# 위 코드의 결과 : {'title': 'sample title', 'author': 'sample author', email: 'sample@email.com'}

# 응답(Response)에 담을 JSON Response Body 생성
content = JSONRenderer().render(serializer.data)
```

<hr/>