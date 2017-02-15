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
For a refresher on editing files with vim see: New User Tutorial: Overview of the Vim Text Editor

visudo

Find the following code:

## Allow root to run any commands anywhere
root ALL=(ALL) ALL

In this case, we’re granting root privileges to the user mynewuser . Add the following below that code:

mynewuser ALL=(ALL) ALL

Then exit and save the file with the command :wq .

If you’ve followed the instruction above correctly, then you should now have a user setup by the name of mynewuser which can use sudo to run commands as root!
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
