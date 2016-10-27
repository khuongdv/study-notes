## Tạo user mới
* Lệnh tạo user mới:
```
useradd songokute
```
* Một vài tham số:
  1. d <homedir>: thay thế đường dẫn mặc định của home, bình thường là /home/songokute mà
  2. g <grupname>: tên group mà user này thuộc về.

* Unlock account bằng cách set password cho nó:
```
passwd songokute
```
* Khi đó shell sẽ hỏi mình điền mật khẩu mới

## Gán quyền

## Thêm SSH key
* Đăng nhập vào user *songokute*
* Nếu tồn tại thư mục .ssh ở home rồi thì:
  ```
  cd .ssh
  ```
  Nếu chưa thì tạo ra rồi cd vào
  ```
  mkdir ~/.ssh rồi
  cd .ssh
  ```
* Mở file này: (dùng *vi* thì chưa có nó tự tạo thêm):
```
vi ~/.ssh/authorized_keys
```
* File này là nơi chứa public key của client mà mình muốn cho vào. Khi đang edit file đó, paste public key vào (lưu ý có newline để ngăn cách với key trước đó)
