## Tìm hiểu Prometheus  
### 1.Prometheus là gì?  
Prometheus là một bộ công cụ giám sát và cảnh báo hệ thống mã nguồn mở ban đầu được xây dựng bởi công ty SoundCloud. Kể từ khi thành lập vào năm 2012, nhiều công ty và tổ chức đã áp dụng Prometheus vào hệ thống và dự án này có một cộng đồng người dùng và nhà phát triển rất tích cực.  
Prometheus bây giờ đã trở thành một dự án mã nguồn mở độc lập và được duy trì độc lập với bất kỳ công ty nào. Prometheus đã tham gia vào tổ chức Cloud Native Computing Foundation vào năm 2016 với tư cách là dự án được ưu tiên phát triển lớn thứ hai, sau Kubernetes (k8s).  
Prometheus có khả năng thu thập thông số/số liệu (metric) từ các mục tiêu được cấu hình theo các khoảng thời gian nhất định, đánh giá các biểu thức quy tắc, hiển thị kết quả và có thể kích hoạt cảnh báo nếu một số điều kiện được thảo mãn yêu cầu.  
Prometheus là 100% mã nguồn mở. Có thể xem mã nguồn tại Git : https://github.com/prometheus/prometheus/  
Phần lớn các core tính năng của Prometheus được viết bằng ngôn ngữ Go. Một số còn lại thì được viết bằng Java, Python hoặc Ruby.  
Prometheus không dùng để lấy dữ liệu log, thay vì vậy thì Prometheus là dịch vụ giám sát, thu thập và xử lý dữ liệu dạng metric (thông số).  
Prometheus sử dụng cơ chế pull dữ liệu từ máy chủ remote là chính, chứ không sử dụng cơ chế đợi remote push dữ liệu lên ngoại trừ trường hợp sử dụng PushGateway.  
Prometheus sử dụng chương trình cảnh báo Alertmanager để xử lý và gửi cảnh báo đi.  
Về phần giao diện biểu đồ thì Prometheus sử dụng mã nguồn Grafana để tích hợp hiển thị.  
Metric của Prometheus sử dụng chuẩn OpenMetrics.  
Prometheus hỗ trợ 3 hình thức cài đặt các thành phần hệ thống gồm : Docker Image, cài đặt từ source với Go và file chương trình chạy sẵn đã được biên dịch sẵn.  
***Một số tính năng của Prometheus***  
-  Mô hình dữ liệu đa chiều với chuỗi dữ liệu theo thời gian.  
-  Cung cấp ngôn ngữ truy vấn dữ liệu - PromQL: tổng hợp dữ liệu chuỗi thời gian trong thời gian thực.  
-  Triển khai đơn giản: bắt đầu từ 1 server duy nhất, có thể mở rộng theo nhu cầu.  
-  Dữ liệu chuỗi thời gian được thu thập qua giao thức HTTP.  
-  Hỗ trợ đẩy dữ liệu thông qua bên thứ 3 trung gian.  
-  Tự động nhận diện mục tiêu hoặc cấu hình tĩnh.  
-  Giao diện người dùng hỗ trợ phong phú, nhiều loại biểu đồ.  
-  Quản lý được trên Cloud và máy chủ vật lý. Được dùng phổ biến để giám sát các hệ thống container và microservices.  

***Mô hình dữ liệu đa chiều***  
Prometheus lưu trữ dữ liệu dưới dạng chuỗi thời gian time series . Chuỗi thời gian là luồng các giá trị theo timestamp của các giá trị được đánh dấu cùng một label hoặc metrics. Label chính là điều tạo nên khả năng đa chiều các dữ liệu trong Prometheus ( phân chia theo host, machine, service ...)  
Ví dụ: muốn giám sát được số lượng HTTP request trên API, chúng ta có thể tạo metric api_http_request_total. Để metric trở nên đa chiều ta sử dụng các label. Label chỉ là các giá trị key-value. Trong trường hợp này ta có thể thêm label method để nhận HTTP method làm giá trị trong metric mới.  
***Ưu điểm và nhược điểm của Prometheus***  

**Ưu điểm**  
-  Độ tin cậy cao. Vì được tích hợp sẵn bằng cách làm cho mỗi máy chủ Prometheus trở nên độc lập với lưu trữ cơ sở dữ liệu chuỗi thời gian cục bộ, để tránh phụ thuộc vào bất kỳ dịch vụ từ xa nào.  
-  Độc lập và không phụ thuộc vào bên ngoài: do đó khi hệ thống có bất kỳ sự có gì, Prometheus vẫn có thể tiến hành giám sát mà không bị gián đoạn.  

**Nhược điểm**  
-  Hơi phức tạp nếu cần mở rộng trong trường hợp đối tượng cần giám sát tăng lên.  
-  Do hoạt động độc lập, nên số lượng các chỉ số giám sát bị phụ thuộc vào sức mạnh cũng như khả năng lưu trữ của máy chủ.  
-  Để giải quyết vấn đề tăng khả năng xử lý cho Prometheus, chúng ta có thể: Nâng cấp phần cứng máy chủ Prometheus. Hoặc giới hạn số lượng chỉ số cần giám sát.  

### 2.Tại sao nó được sinh ra?  
Do công việc Development và Operations ngày càng trở lên áp lực vì hệ thống là sự tổng hợp vô số các thành phần khác nhau và có các nhu cầu quản trị, điều hành, bảo trì,...  Ví dụ trong môi trường containerized như Docker, Kubernetes, khi có vô số máy chủ chạy hàng ngàn container và có sự liên kết lẫn nhau thì việc đảm bảo cho hệ thống ổn định, vận hành trơn tru là một nhiệm vụ khá khó. 
Prometheus được sinh ra để giải quyết 1 số vấn để sau:  
-  Giám sát hệ thống phân tán.  
-  Giám sát tình trạng máy chủ: CPU, memory, hdd, lỗi hệ thống, server ngừng hoạt động,...  
-  Giám sát các chương trình phần mềm: lỗi phần mềm, độ trễ,...  
-  Nhanh chóng nhận diện sự cố, nguồn gốc phát sinh, cung cấp thông tin cụ thể cho developer kịp thời xử lý.  
-  Tự động giám sát và đưa ra cảnh báo.  

**Hệ thống phân tán là gì ?**  
Hệ thống phân tán là một hệ thống bao gồm nhiều thành phần hoạt động đôc lập, trao đổi và làm việc với nhau (qua mạng) để giải quyết một vấn đề cụ thể.  
Các thành phần trong hệ thống phân tán có thể là một máy tính (máy vật lý hoặc máy ảo), container, hay bất kỳ thiết bị kết nối mạng nào, có bộ nhớ local và có thể giao tiếp với nhau thông qua mạng máy tính.  

### 3.Nó hoạt động như thế nào? Luồng hoạt động với các thành phần khác trong stack ra sao?  
***Cách Prometheus hoạt động:***  
Prometheus thực hiện quá trình kéo(pull) các thông số/số liệu(metric) từ các job(exporter) được chỉ định qua kênh trực tiếp hoặc thông qua dịch vụ Pushgateway trung gian. Sau đó Prometheus sẽ kưu các dữ liệu thu thập được ở local máy chủ. Tiếp đến sẽ chạy các rule để xử lý các dữ liệu theo nhu cầu cũng như kiểm tra thực hiện các cảnh báo mà ta mong muốn.  

<img src="https://github.com/vuducthanh0115/img/blob/main/anh/img1.png" width="800" height="400" />  

Đầu tiên thì job(exporter) sẽ giúp lấy các thông số sau đó theo định kì 1 thời gian nhất định thì Prometheus sẽ thu thập bằng cách kéo các thông số đã được lấy ra về và lưu vào trong database. Từ dữ liệu của database Prometheus có thể xây dựng những biểu đồ trên trang web để ta có thể dễ dàng theo dõi và Prometheus hỗ trợ việc theo dõi và cảnh báo giúp ta giám sát hệ thống. Chúng ta có thể sử dụng Grafana hoặc Prometheus để gửi cảnh báo qua mail, pagerduty, sky, ...  

**Exporters**  
Exporter về cơ bản như là 1 loại hình dịch vụ (Services) có khả năng thu thập các chỉ số từ đối tượng cần giám sát, sau đó chuyển đổi thành định dạng mà Prometheus có thể hiểu. Exporter cũng cung cấp 1 địa chỉ Endpoint đúng theo yêu cầu mà Prometheus cần.  
Danh sách exporter trải dài từ cơ sở dữ liệu (MongoDB, MySql, PostgreSQL,...), phần cứng (NVIDIA GPU, Fortigate, Netgear Router, IoT Edison,...), lưu trữ (Hadoop HDFS FSImage, ScaleIO, GPFS, Gluster,...), máy chủ web (Apache, Nginx, HAProxy,...), hoặc là các nền tảng đám mây như AWS, Cloudflare, DigitalOcean,...  
**Exporter lấy metrics rồi đẩy ra đâu?**  
Exporter giúp thu thập các chỉ số từ đối tượng cần giám sát, sau đó chuyển đổi thành định dạng mà Prometheus có thể hiểu. Sau đó đẩy các metrics về service của Prometheus.  

**Client Libraries**  
Prometheus cung cấp bộ thư viện được viết bằng rất nhiều ngôn ngữ lập trình như Go, Java, NodeJS, Ruby, C++, C#,...  
Thư viện này giúp chúng ta tạo ra endpoint “/metrics” theo nhu cầu riêng, và định dạng dữ liệu theo chuẩn mà Prometheus có thể hiểu và xử lý.  

**Endpoint**: nguồn dữ liệu của các chỉ số (metric) mà Prometheus sẽ đi lấy thông tin.  

**Push Gateway Prometheus**: sử dụng để hỗ trợ các job có thời gian thực hiện ngắn (tạm thời).  Đơn giản là các tác vụ công việc này không tồn tại lâu đủ để Prometheus chủ động lấy dữ liệu. Vì vậy là mà các dữ liệu chỉ số (metric) sẽ được đẩy về Push Gateway rồi đẩy về Prometheus Server.  

### 4.Alert rule là gì?  
Alert rule là các quy tắc cảnh báo được đặt ra để xác định những chỗ phá vỡ quy tắc này và gửi cảnh báo đến Alertmanager. Alert rule chạy cùng ngay trong service Prometheus. Alertmanager sẽ quản lý các cảnh báo (alert), xử lý nội dung alert nếu có tuỳ biến này và điều hướng đầu tiếp nhận thông tin cảnh báo như email,sky, call,…  
Alerts rule là một dạng record rule đặc biệt khi mà kết quả của biểu thức sẽ là cơ sở để tạo alert của Prometheus gửi đi alertmanager  


