# View trong Django

Trong Django, View đóng vai trò như Controller trong mô hình MVC. Nó được chạy khi khi truy cập một địa chỉ có dạng nhất định để phản hồi và hiển thị một trang web nhất định.

Controller được biểu diễn dưới dạng một hàm (controller dạng hàm) hoặc class (controller dạng class). Dạng đầu linh hoạt hơn, nhưng thường tốn công sức trong lập trình, cái sau cho phép bạn thực hiện các tác vụ điển hình như hiển thị danh sách với số mã tối thiểu.

Mô-đun `views.py` được tạo trong mỗi gói ứng dụng, được xem là nơi chính thức để chứa các controller. Tuy nhiên, không có gì ngăn cản chúng ta đặt controller ở một mô-đun khác.

Hãy viết một controller hiển thị... không phải là danh sách các quảng cáo - chúng ta chưa có danh sách này, hiện tại chỉ có văn bản thông báo những gì khách truy cập trong tương lai sẽ thấy trên trang này: là một danh sách các quảng cáo.

Ở mô-đun `views.py` của gói ứng dụng `bboard`, xóa mã nhỏ ở đó và thay bằng mã dưới đây:

```python
from django.http import HttpResponse

def index(request):
    return HttpResponse("Một danh sách các quảng cáo sẽ được hiển thị ở đây.")
```

Controller của chúng ta thực sự là hàm `index()`. Điều duy nhất nó làm là gửi một thông báo văn bản cho khách hàng: "Một danh sách các quảng cáo sẽ được hiển thị ở đây.".

Mọi controller dạng hàm đều chỉ yêu cầu một đối số duy nhất, là một đối tượng `HttpRequest`, đối tượng này lưu trữ nhiều thông tin khác nhau về yêu cầu đã nhận: địa chỉ, dữ liệu nhận được từ khác truy cập, thông tin dịch vụ từ trình duyệt web...Theo truyền thống, tham số này được đặt tên là `request`. Trong ví dụ trên, chúng ta chưa sử dụng đến tham số `request` này.

Trong thân hàm, chúng ta tạo một đối tượng `HttpResponse` (được lấy từ mô-đun `django.http`), đối tượng này biểu diễn cho phản hồi được gửi đến máy khách. Nội dung của phản hồi này - chính là thông báo văn bản - được chỉ định bởi đối số của hàm tạo. Chúng ta sẽ trả về đối tượng này.