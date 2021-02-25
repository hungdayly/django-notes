# Tạo một ứng dụng Django

Trong Django, một ứng dụng là một phần chức năng riêng biệt của trang web đang được phát triển, ít nhiều độc lập với các ứng dụng khác của dự án.

Bất kỳ ứng dụng nào cũng được biểu diễn bằng một gói Python thông thường (*gói dứng dụng*), chứa các mô-đun. Gói này nằm trong thư mục dự án, cùng cấp với gói cấu hình của dự án. Tên của gói sẽ trở thành tên của chính ứng dụng.

Tạo một ứng dụng mới có tên `bboard` bằng lệnh `startapp` được cung cấp bởi `manage.py`:

```bash
cd ~/django-notes
~/django-notes
$ source venv/Scripts/activate
(venv) ~/django-notes
cd samplesite
(venv) ~/django-notes/samplesite
$ python manage.py startapp bboard
```

Ứng dụng này sẽ đảm nhận chức năng hiển thị danh sách các quảng cáo do khách truy cập đăng.

Một thư mục cùng tên với ứng dụng được tạo ra trong thư mục dự án. Trong đó có các tệp và thư mục sau:

- `migrations`: là nơi lưu trữ các migration mà ta tạo ra đối với model. Thư mục này ban đầu chỉ chứa file `__init__.py` trống, đánh dấu rằng nó là một gói Python hoàn chỉnh.
- `__init__.py`: tệp này cho Python biết thư mục này là một gói (*gói ứng dụng*).
- `admin.py`: mô-đun cài đặt Django Admin cho ứng dụng.
- `apps.py`: mô-đun với các cài đặt của ứng dụng.
- `models.py`: mô-đun chứa các mô hình dữ liệu của ứng dụng.
- `tests.py`: mô-đun chứa các thủ tục kiểm tra.
- `views.py`: mô-đun chứa các controller (thuật ngữ trong mô hình MVC), trong Django controller gọi là view.

Hãy đăng ký ứng dụng mới tạo tạo trong dự án. Hãy tìm tệp `settings.py` (trong *gói cấu hình* dự án), mở nó trong trình soạn thảo văn bản và tìm đoạn mã sau:

```python
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Danh sách, được lưu trữ trong biến `INSTALLED_APPS`, liệt kê tất cả các ứng dụng đã đăng ký với dự án và tham gia vào công việc của nó. Ban đầu, danh sách này chỉ chứa các ứng dụng tiêu chuẩn là một phần của Django và thực thi các chức năng tích hợp sẵn của framework. Chẳng hạn, ứng dụng `django.contrib.auth` thực thi chức năng kiểm soát truy cập, và ứng dụng `django.contrib.sessions` thực thi chức năng quản lý các session của máy chủ.

Danh sách này hiện tại chưa có ứng dụng của chúng ta. Hãy thêm nó bằng cách thêm một phần tử mới vào trong danh sách:

```python
INSTALLED_APPS = [
    ...
    'bboard.apps.BboardConfig',
]
```

Chúng ta đã chỉ định một dòng có đường dẫn đến class `BboardConfig` trong mô-đun `apps` của ứng dụng.

```python
# bboard/apps.py

from django.apps import AppConfig


class BboardConfig(AppConfig):
    name = 'bboard'
```

Class `BboardConfig` thừa kế từ class `AppConfig` được lấy từ mô-đun `django.apps`, hiện tại có một thuộc tính duy nhất có tên `name` lưu tên của ứng dụng.
