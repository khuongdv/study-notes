## Giới thiệu
- Khái niệm "Microservices" mô tả một pattern trong phát triển phần mềm, ngày càng nổi lên là xu hướng mới bởi nhu cầu tăng tốc độ và hiệu quả của việc phát triển và quản lý giải pháp phần mềm. 

## What are microservices
- Microservices là cách thức áp dụng việc phân rã ứng dụng thành các services đơn nhiệm, ít ràng buộc với nhau, nhằm deliver và maintain hệ thống phần mềm phức tạp trong bối cảnh ngày nay.
- Microservices chia nhỏ ứng dụng (thường được đóng gói lại thành 1 gói) thành các ứng dụng nhỏ và đơn giản hơn. Mỗi ứng dụng nhỏ sẽ làm một việc, và đương nhiên là phải làm tốt việc của nó. Lý giải vì sao lại có chữ "micro"
- Mỗi ứng dụng nhỏ được phát triển bởi những đội chuyên trách. Điều này giảm thiểu nguy cơ tiềm ẩn trong việc giao tiếp giữa các đội trong lúc phát triển. Microservices có thể ko phù hợp với những ứng dụng đơn giản, nhưng sẽ rất tốt cho việc phát triển một công trình phức tạp lớn nhanh.
- Khái niệm đằng sau microservices tương tự như SOA (kiến trúc hướng dịch vụ), vì thế việc sử dụng microservices được coi như "SOA with DevOps" hoặc "SOA 2.0"

## Đặc tính quan trọng của Microservices
1. __Thiết kế hướng domain__: Phân rã theo chức năng có thể làm dễ dàng bằng cách sử dụng phương pháp Eric Evans's DDD
2. __Nguyên lý đơn nhiệm__: Mỗi dịch vụ chỉ chịu trách nhiệm cho một phần đơn lẻ của tính năng và làm tốt việc đơn lẻ đó
3. __Giao tiếp qua giao diện được quy định rõ ràng__
4. __Độc lập về việc triển khai, cập nhật, thay thế hoặc mở rộng__ (DURS - Deploy, Update, Replace, Scale)
5. __Giao tiếp gọn nhẹ__: REST qua HTTP hoặc STOMP qua WebSocket

## Các lợi ích mà microservices đem lại
1. __Độc lập mở rộng__: Mỗi microservice có thể mở rộng 1 cách độc lập thông qua việc thêm CPU hoặc thêm bộ nhớ (mở rộng chiều X)
hoặc là sharding (mở rộng chiều Y), tùy vào nhu cầu. Rất khác so với ứng dụng nguyên khối, loại nguyên khối này có nhiều yêu cầu khác
cần phải được triển khai cùng nhau
2. __Độc lập lên phiên bản__: Mỗi service có thể được triển khai độc lập với các dịch vụ khác. Mọi thay đổi trên 1 dịch vụ thì có thể
được tạo ra bởi đội chuyên trách của service đó, ko cần phải có sự sắp xếp nào với đội khác.
3. __Dễ bảo trì__: code của microservice giới hạn trong 1 hàm và vì thế dễ hiểu hơn. IDEs khi đó chỉ cần load lượng code ít hơn và dễ hơn,
giú tăng khả năng đọc code và làm cho dev năng suất hơn :)
4. __Chọn công nghệ/nền tảng/framework__ tối ưu cho nhu cầu của service đó và tùy thuộc vào đội dev
5. __Cô lập lỗi và tài nguyên__: Một dịch vụ có những dấu hiệu như memory leak, kết nối đến DB ko được đóng,... sẽ chỉ ảnh hưởng đến service
đó. Điều này ngược lại với ứng-dụng-nguyên-khối (monolithich application)

## Operational Requirements for Microservices
Microservices không phải là luôn phù hợp giải quyết mọi vấn đề về kiến trúc trong các ứng dụng của bạn.

1. Các service cần được chỉ ra cách __replicate__, (nhân đôi theo chiều X hoặc chia nhỏ theo chiều Y). Cần có cơ chế chuẩn sử dụng metadata cho việc scale

2. __Service discovery__: Trong thế giới microservice, nhiều services thường được phân bố trong 1 môi trường PaaS. Hạ tầng cố định
được cung cấp bởi các containers hoặc các máy ảo cố định. Các services có thể được mở rộng dựa vào vài metrics định trước.

 Mỗi dịch vụ đăng kí với broker và cung cấp chi tiết về dịch vụ đó (gồm cả endpoint address). Các consumers truy vấn broker rồi tìm dịch vụ nó cần rồi gọi. Và cách để đăng kí và truy vấn dịch vụ như ZooKeeper, Kubernetes...

3. __Service monitoring__: 
Một khía cạnh quan trọng của hệ thống phân tán là giám sát và ghi log cho service. Khi đó ta sẽ chủ động có action khi một dịch vụ tiêu tốn tài nguyên một cách bất thường. ELK Stack có thể tổng hợp log từ nhiều microservices, trực quan hóa dữ liệu đó lên.

4. __Resiliency__: Software failure will occur, no matter how much and how hard you test. This is all the more important when multiple microservices are distributed all over the Internet. The key concern is not “how to avoid failure” but “how to deal with failure.” It’s important for services to automatically take corrective action to ensure user experience is not impacted. The Circuit Breaker pattern allows one to build resiliency in software—Netflix’s Hystrix and Ribbon are good libraries that implement this pattern

5. __DevOps__: Continuous Integration and Continuous Deployment (CI/CD) are very important in order for microservices-based applications to succeed. These practices are required so that errors are identified early, and so little to no coordination is required between different teams building different microservices.

## Những nguyên lý thiết kế tốt cho các ứng dụng nguyên khối
Refactoring a monolith into a microservices-based application will not help solve all architectural issues. Before you start breaking up a monolith, it’s important to make sure the monolith is designed following good software architecture principles. Some common rules are:

 1. Practice separation of concerns, possibly using Model-View- Controller (MVC)
 2. Use well-defined APIs for high cohesion and low coupling
 3. Don’t Repeat Yourself (DRY)
 4. Use Convention over Configuration (CoC)
 5. Separate interfaces/APIs and implementations, and follow the Law of Demeter. Classes shouldn’t call other classes directly just because they happen to be in the same archive
 6. Use Domain-Driven Design to keep objects related to a domain/component together
 7. Don’t build something that you don’t need now (YAGNI—You Aren’t Going to Need It)

## Refactor ứng dụng nguyên khối thành hệ thống các microservices
Consider a Java EE monolithic application that is typically defined as a WAR or an EAR archive. The entire functionality for the application is packaged in a single unit. For example, an online shopping cart may consist of User, Catalog, and Order functionalities. All web pages are in the root of the application, all corresponding Java classes are in the WEB-INF/classes directory, and all resources are in the WEB-INF/classes/META-INF directory.

Such an application can be refactored into microservices, which would create an architecture that would look like the following:

 - The above application is functionally decomposed where User, Order, and Catalog components are packaged as separate WAR files. Each WAR file has the relevant web pages, classes, and configuration files required for that component.
 - Java EE is used to implement each component, but there is no long term commitment to the stack, as different components talk to each other using a well-defined API.
 - Different classes in this component belong to the same domain, so the code is easier to write and maintain. The underlying stack can also change, possibly keeping technical debt to a minimum.
 - Each archive has its own database (i.e. data stores are not shared). This allows each microservice to evolve and choose whatever type of data store—relational, NoSQL, flat file, in- memory, or some thing else—is most appropriate.
 - Each component registers with a Service Registry. This is required because multiple stateless instances of each service might be running at a given time, and their exact endpoint locations will be known only at the runtime. Netflix Eureka, etcd, and Zookeeper are some options for service registry/ discovery.
 - If components need to talk to each other, which is quite common, then they would do so using a pre-defined API. REST for synchronous or Pub/Sub for asynchronous communication are the most common means to achieve this. In this case, the Order component discovers User and Catalog service and talks to them using a REST API.
 - Client interaction for the application is defined in another application (in this case, the Shopping Cart UI). This application discovers the services from the Service Registry and composes them together. It should mostly be a dumb proxy (discussed in a later section), where the UI pages of the different components are invoked to display the interface. A common look and feel can be achieved by providing standard CSS/ JavaScript resources

## Patterns trong microservices
1. Use Bounded Contexts to Identify Candidates for Microservices

2. Designing Frontends for Microservices

3. Use an API Gateway to Centralize Access to Microservices

4. Database Design and Refactorings

5. Packaging and Deploying Services

6. Event-driven architecture

7. Consumer-Driven Contract Testing

## Tổng kết
Microservices có nhiều lợi ích và tất nhiên giúp công việc của bạn phát triển nhanh hơn. Nhưng mấy ứng dụng nguyên khối cũng có thể đã làm khá tốt. Cân nhắc các yêu cầu về operational cho microservices và các lợi ích có được khi chuyển sang microservices, trước khi refactor hệ thống nguyên khối hiện tại của mình.
