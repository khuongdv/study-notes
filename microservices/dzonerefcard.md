## Giới thiệu
- Khái niệm "Microservices" mô tả một pattern trong phát triển phần mềm, ngày càng nổi lên là xu hướng mới bởi nhu cầu tăng tốc độ và hiệu quả
của việc phát triển và quản lý giải pháp phần mềm. 

## What are microservices
- Microservices là cách thức áp dụng việc phân rã ứng dụng thành các services đơn nhiệm, ít ràng buộc với nhau, nhằm deliver và maintain hệ
thống phần mềm phức tạp trong bối cảnh ngày nay.
- Microservices chia nhỏ ứng dụng (thường được đóng gói lại thành 1 gói) thành các ứng dụng nhỏ và đơn giản hơn. Mỗi ứng dụng nhỏ sẽ 
làm một việc, và đương nhiên là phải làm tốt việc của nó. Lý giải vì sao lại có chữ "micro"
- Mỗi ứng dụng nhỏ được phát triển bởi những đội chuyên trách. Điều này giảm thiểu nguy cơ tiềm ẩn trong việc giao tiếp giữa các đội
trong lúc phát triển. Microservices có thể ko phù hợp với những ứng dụng đơn giản, nhưng sẽ rất tốt cho việc phát triển một công trình
phức tạp lớn nhanh.
- Khái niệm đằng sau microservices tương tự như SOA (kiến trúc hướng dịch vụ), vì thế việc sử dụng microservices được coi như "SOA with DevOps"
hoặc "SOA 2.0"

## Đặc tính quan trọng của Microservices
1. Thiết kế hướng domain: Phân rã theo chức năng có thể làm dễ dàng bằng cách sử dụng phương pháp Eric Evans's DDD
2. Nguyên lý đơn nhiệm: Mỗi dịch vụ chỉ chịu trách nhiệm cho một phần đơn lẻ của tính năng và làm tốt việc đơn lẻ đó
3. Giao tiếp qua giao diện được quy định rõ ràng
4. Độc lập về việc triển khai, cập nhật, thay thế hoặc mở rộng (DURS - Deploy, Update, Replace, Scale)
5. Giao tiếp gọn nhẹ: REST qua HTTP hoặc STOMP qua WebSocket

## Các lợi ích mà microservices đem lại
1. Độc lập mở rộng: Mỗi microservice có thể mở rộng 1 cách độc lập thông qua việc thêm CPU hoặc thêm bộ nhớ (mở rộng chiều X)
hoặc là sharding (mở rộng chiều Y), tùy vào nhu cầu. Rất khác so với ứng dụng nguyên khối, loại nguyên khối này có nhiều yêu cầu khác
cần phải được triển khai cùng nhau
2. Độc lập lên phiên bản: Mỗi service có thể được triển khai độc lập với các dịch vụ khác. Mọi thay đổi trên 1 dịch vụ thì có thể
được tạo ra bởi đội chuyên trách của service đó, ko cần phải có sự sắp xếp nào với đội khác.
3. Dễ bảo trì: code của microservice giới hạn trong 1 hàm và vì thế dễ hiểu hơn. IDEs khi đó chỉ cần load lượng code ít hơn và dễ hơn,
giú tăng khả năng đọc code và làm cho dev năng suất hơn :)
4. Chọn công nghệ/nền tảng/framework tối ưu cho nhu cầu của service đó và tùy thuộc vào đội dev
5. Cô lập lỗi và tài nguyên: Một dịch vụ có những dấu hiệu như memory leak, kết nối đến DB ko được đóng,... sẽ chỉ ảnh hưởng đến service
đó. Điều này ngược lại với ứng-dụng-nguyên-khối (monolithich application)

## Operational Requirements for Microservices
Microservices không phải là luôn phù hợp giải quyết mọi vấn đề về kiến trúc trong các ứng dụng của bạn.

1. Các service cần được chỉ ra cách replicate, (nhân đôi theo chiều X hoặc chia nhỏ theo chiều Y). Cần có cơ chế chuẩn sử dụng metadata
cho việc scale
2. Service discovery: Trong thế giới microservice, nhiều services thường được phân bố trong 1 môi trường PaaS. Hạ tầng cố định
được cung cấp bởi các containers hoặc các máy ảo cố định. Các services có thể được mở rộng dựa vào vài metrics định trước.

 Mỗi dịch vụ đăng kí với broker và cung cấp chi tiết về dịch vụ đó (gồm cả endpoint address). Các consumers truy vấn broker rồi tìm dịch vụ nó cần rồi gọi. Và cách để đăng kí và truy vấn dịch vụ như ZooKeeper, Kubernetes...

3. Service monitoring: 
