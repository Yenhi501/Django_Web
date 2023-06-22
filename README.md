# Django_Web
Cài đặt Django
Ở đây chúng ta cài đặt thông qua virtualenv và pip nha. Chú ý là hướng dẫn cài đặt này chỉ dùng trên ubuntu thôi nhé
mọi người. Để cài đặt django thì các bạn sử dụng gói combo thần thánh sau đây:

$ sudo apt-get update && sudo apt-get install python-virtualenv python-pip build-essential
python-dev libffi-dev libssl-dev libxml2-dev libxslt1-dev postgresql python-psycopg2 -y
$ mkdir django-framework
$ cd mdjango-framework
$ virtualenv -p python3 djangotut
$ djangotut/bin/pip install django

Folder django-framework sẽ là nơi chúng ta thực thi django. Và trước khi code với django thì chỉ cần
source djangotut/bin/activate trong terminal là được.

Tạo project demo
Để render ra 1 template với full cấu trúc cho django project thì các bạn chỉ cần chạy lệnh
django-admin startproject project_name sau khi đã active virtualenv.

Chú ý: Không đặt tên project là django hoặc test. Và không như PHP đặt code ở /var/www
Django sẽ tránh đặt ở các folder root, để bảo mật code. Bạn có thể đặt code ở /home/xxx

Ở đây mình đặt tên project là demo_django, và sau khi chạy lệnh trên thì mình có được 1 folder với cấu trúc như sau:

demo_django
...manage.py
...demo_django
......__init__.py
......settings.py
......urls.py
......wsgi.py

Những file trong này đều có 1 chức năng riêng và cụ thể nó sẽ như sau:

__init__.py là 1 file rỗng chỉ định việc cái đường dẫn folder này sẽ được xem như là 1 Python package.
settings.py là file chứa các settings của project. Trong file này chứa các setting cơ bản như DEBUG, ALLOWED_HOSTS, INSTALLED_APP, DATABASES, ...
urls.py là file khai báo các URL của project (kiểu như routing, với địa chỉ nào thì sẽ thực thi hàm nào).
wsgi.py là file dùng deploy project lên server.
manage.py là file để tạo app, migrate,...
Bây giờ các bạn có thể chạy lệnh python manage.py runserver và vào link http://127.0.0.1:8000/ để thấy điều kỳ diệu nha.
Now let's create own first app ✌️

Tạo app đầu tiên
Để tạo 1 app thì các bạn cần phải vào cùng thư mục với file manage.py và chạy lệnh python manage.py startapp your_app_name
Ở đây thì mình sẽ tạo 1 app tên là mypage => câu lệnh của mình sẽ là: python manage.py startapp mypage. Và cấu trúc folder mypage mới tạo của mình sẽ như sau:

mypage/
...__init__.py
...admin.py
...apps.py
...migrations/
......__init__.py
...models.py
...tests.py
...views.py

Tạo view
Các bạn mở file views.py vừa mới tạo trong thư mục mypage lên và thêm vào đoạn sau:

from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello all, it's my first page.")

Sau đó bạn cần config lại URL bằng cách tạo thêm file urls.py trong thư mục mypage.
Trong này sẽ chứa những config url dành cho app mypage.

from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]

Tiếp theo bạn thêm đoạn code sau vào file urls.py của thư mục demo_django để thực hiện việc trỏ rootURL
đến module mypage.urls.

from django.urls import include, path
from django.contrib import admin

urlpatterns = [
    path('mypage/', include('mypage.urls')),
    path('admin/', admin.site.urls),
]

Cuối cùng các bạn run lại server bằng lệnh python manage.py runserver và vào link http://127.0.0.1:8000/mypage/ để cảm nhận thành quả.
