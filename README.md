dfjago-admin startproject myproject cd my project

poython manage.py startapp board
앱 설정하기

url 
 from django.urls import path
 from . import views



from django.contrib import admin
from django.urls import path

import board.views
import product.views
import reply.views
import user.views

urlpatterns = [
    path('admin/', admin.site.urls),

    path('board/create',board.views.create),
    path('board/listGet',board.views.listGet),
    path('board/readGet/<int:bid>',board.views.readGet),
    path('board/deleteGet/<int:bid>',board.views.deleteGet),
    path('board/update/<int:bid>',board.views.update),

    path('reply/create',reply.views.create),
    path('reply/list',reply.views.list),
    path('reply/read/<int:rid>',reply.views.read),
    path('reply/delete/<int:rid>',reply.views.delete),
    path('reply/update/<int:rid>',reply.views.update),

    path('user/signup', user.views.singup),
    path('user/login', user.views.login),
    path('user/logout', user.views.logout),

]

from django import forms

from board.models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post # model은 Post 양식으로 쓰겠다.
        fields = ('title', 'contents') # 어떤 필드를 입력 받을 지
        exclude = ('writer', ) # 폼에서 writer 입력받지 않게 함


        <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!-- authenticated가 되어있으면(True) 글씨를 뜨게 함-->
{% if request.user.is_authenticated%}
로그인 한 사용자 : {{ request.user }} <br/>
{% endif %}

{% for post in posts %}
    {{ post.id }}
<!-- postid에 해당하는 contents를 클릭하면 해당 id의 readGet으로 이동 -->
    <a href="readGet/{{ post.id }}"> {{ post.contents }} </a>
    {{ post.writer }}
<br/>
{% endfor %}
<a href="../board/create">게시글 작성</a>
</body>
</html>


