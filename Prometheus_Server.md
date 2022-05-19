# Tổng quan Prometheus Server  
## Giới thiệu cơ bản về Prometheus  
### Monitoring là gì? Khác gì với Logging và Tracing  
Monitoring là quá trình thu thập, tổng hợp và phân tích các số liệu(metrics) để cải thiện hệ thống.  
Logging là hệ thống thu thập, tìm kiếm, phân tích,... log của ứng dụng  
Tracing là các hệ thống theo dõi đường đi của 1 request tới hệ thống. Nó đi qua những service nào, dừng ở mỗi service bao lâu, lỗi ở step nào,...  

### Prometheus là gì?
Prometheus là một bộ công cụ giám sát và cảnh báo hệ thống mã nguồn mở ban đầu được xây dựng bởi công ty SoundCloud.  
Prometheus bây giờ đã trở thành một dự án mã nguồn mở độc lập và được duy trì độc lập với bất kỳ công ty nào.  
Prometheus có khả năng thu thập thông số/số liệu (metric) từ các mục tiêu được cấu hình theo các khoảng thời gian nhất định, đánh giá các biểu thức quy tắc, hiển thị kết quả và có thể kích hoạt cảnh báo nếu một số điều kiện được thảo mãn yêu cầu.  
Prometheus là 100% mã nguồn mở. Có thể xem mã nguồn tại Git : https://github.com/prometheus/prometheus/  
Phần lớn các core tính năng của Prometheus được viết bằng ngôn ngữ Go. Một số còn lại thì được viết bằng Java, Python hoặc Ruby.  
Prometheus không dùng để lấy dữ liệu log, thay vì vậy thì Prometheus là dịch vụ giám sát, thu thập và xử lý dữ liệu dạng metric (thông số).  
Prometheus sử dụng cơ chế pull dữ liệu từ máy chủ remote là chính, chứ không sử dụng cơ chế đợi remote push dữ liệu lên ngoại trừ trường hợp sử dụng PushGateway.  
Prometheus sử dụng chương trình cảnh báo Alertmanager để xử lý và gửi cảnh báo đi.  

### Các khái niệm cơ bản của Prometheus    
**Data model**  
Prometheus về cơ bản lưu trữ tất cả dữ liệu dưới dạng time series. Time series là luồng các giá trị theo timestamp của các giá trị được đánh dấu cùng một label hoặc metrics.  
***Metric names and labels***  
Mỗi time series được xác định duy nhất bởi tên metric name và một bộ các cặp key-value được gọi là labels(nhãn).
Metric name chỉ định các thông số của của hệ thống. Vd: http_requests_total - tổng số request HTTP đã nhận). Nó có thể chứa các chữ cái và chữ số ASCII cũng như dấu gạch dưới và dấu hai chấm. Nó phải được match với [a-zA-Z_:][a-zA-Z0-9_:]*.  
Labels: bất kỳ sự kết hợp nhãn đã cho nào cho cùng một metric name xác định particular dimensional instantiation of that metric( Vd: tất cả HTTP requests đã sử dụng phương thức POST tới /api/tracks xử lý). Ngôn ngữ truy vấn cho phép lọc và tổng hợp dựa trên các labels này. Khi thay đổi giá tri label, bao gồm cả thêm hoặc xóa label sẽ tạo ta một time series mới.  
Ví dụ: 
``` 
api_http_requests_total{method="POST", handler="/messages"}  
```  
Một time series có metric name là api_http_requests_total và lable method="POST", handler="/messages   

**Metric types**  
***Có 4 kiểu metric được sử dụng trong prometheus:***  
- **Counter** là một bộ đếm tích lũy, được đặt về 0 khi restart. Ví dụ, có thể dùng counter để đếm số request được phục vụ, số lỗi, số task hoàn thành,... Không sử dụng cho gía trị có thể giảm như số tiến trình đang chạy. Trong trường hợp này, ta có thể sử dụng gauge.  
- **Gauge** đại diện cho số liệu duy nhất, nó có thể lên hoặc xuống. Nó thường được sử dụng cho các giá trị đo.  
- **Histogram** lấy mẫu quan sát (thường là những thứ như là thời lượng yêu cầu, kích thước phản hồi). Nó cũng cung cấp tổng của các giá trị đó.  
- **Summary** tương tự histogram, nó cung cấp tổng số các quan sát và tổng các giá trị đó, nó tính toán số lượng có thể cấu hình qua sliding time window.  

**Jobs và Instances**  
Trong prometheus quy định một endpoint mà chúng ta có thế thể scrape được gọi là một **instance**.  
Tập hợp của các instances có cùng một mục đích được gọi là một **job**.  
Ví dụ:  
job: api-server  
instance 1: 1.2.3.4:5670  
instance 2: 1.2.3.4:5671  
instance 3: 5.6.7.8:5670  
instance 4: 5.6.7.8:5671  

### Kiến trúc của Prometheus stack và các thành phần cơ bản.  

#### Các thành phần trong promtheus  

Hệ sinh thái của giải pháp bao gồm nhiều thành phần trong đó có một vài thành phần là tùy chọn ( tức là có thể có hoặc không )  

- **Prometheus server** để  scrapes và lưu trữ dữ liệu 
- **Client libraries** hỗ trợ các ngôn ngữ lập trình khác tương tác với prom 
- **Push gateway** là một gateway trung gian hỗ trợ short-lived jobs 
- Các **exporter** để giám sát các services như HAProxy, StatsD, Graphite, ... 
- Một **alertmanager** phụ vụ cho việc cảnh báo 

## 4. Kiến trúc của Prometheus  

Sơ đồ này minh họa kiến ​​trúc của Prometheus và một số thành phần trong hệ sinh thái của nó:

<div style="text-align:center"><img src="https://prometheus.io/assets/architecture.png"></div>

Cách làm việc của promtheus được mô tả như sau:  

- Metrics sẽ thu thập thông qua exporter 
- Prometheus sẽ tự discovery ra target của các jobs hoặc trong file cấu hình thủ công để pull metrics về 
- Sau đó prom server sẽ xử lý và lưu trữ xuống database của mình
- Cùng lúc đó AlertManager sẽ tiến hành kiểm tra điều kiện nếu match với các rules đã được người quản trị định nghĩa thì sẽ gửi cảnh báo thông qua các kênh mail, slack, ... 
- Prom UI là nơi hiển thị graph của các metrics đẩy về hệ thống. Ngoài ra garafa cũng hỗ trợ data source prom. 

Prom được viết bằng ngôn ngữ Go và được thiết kế theo kiến trúc microservices. Các thầnh phần của nó giao tiếp với nhau thông qua api 

#### Trường hợp nào sử dụng Prometheus ?

Prometheus hoạt động tốt để ghi các time series data dạng số. Nó phù hợp với việc giám sát các máy chủ cũng như các kiến trúc highly dynamic service-oriented.

Đối với microservice, nó hỗ trợ thu thập và truy vấn dữ liệu đa chiều.

#### Trường hợp nào không nên sử dụng?

Prometheus là đáng tin cậy. Có thể xem thống kê nào có sẵn về hệ thống của chúng ta, ngay cả trong điều kiện lỗi. Nếu chúng ta cần độ chính xác 100%, ví dụ cho mục đích thanh toán, Prometheus không phải là một lựa chọn tốt vì nó không chi tiết và đầy đủ.

### Cấu hình Prometheus  

#### Cấu hình Prometheus server  

#### Recording rules

Các recording rules cho phép ta định tuyến trước các biểu thức thường xuyên cần thiết hoặc expensive về mặt tính toán và lưu kết quả của chúng dưới dạng một chuỗi time series mới. Truy vấn kết quả được tính trước sau đó thường sẽ nhanh hơn nhiều so với thực hiện biểu thức ban đầu mỗi khi cần thiết. Điều này đặc biệt hữu ích cho bảng điều khiển, cần truy vấn cùng một biểu thức lặp đi lặp lại mỗi khi chúng làm mới. 

Các recording rules và alerting rules tồn tại trong 1 nhóm rule. Các rule trong một nhóm được chạy tuần tự trong một khoảng thời gian đều đặn, với cùng một evaluation time. Tên của các recording rules phải là metric name hợp lệ. Tên của các alerting rules phải là giá trị label(nhãn) hợp lệ. 

Cú pháp của tệp quy tắc là: 
```
groups:
  [ - <rule_group> ] 
```
Một tệp quy tắc ví dụ đơn giản : 
```
groups:
  - name: example
    rules:
    - record: job:http_inprogress_requests:sum
      expr: sum by (job) (http_inprogress_requests)
<rule_group>

name: <string>

[ interval: <duration> | default = global.evaluation_interval ]

rules:
  [ - <rule> ... ] 
```

Cú pháp cho recording rules là: 
```
record: <string>

expr: <string> 

labels:
  [ <labelname>: <labelvalue> ] 
```
<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/recording%20rules.png"></div>  

<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/recording%20rules_2.png"></div>  

<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/recording%20rules_3.png"></div>

#### Alerting rules

Cho phép ta xác định các điều kiện cảnh báo dựa trên biểu thức ngôn ngữ của Prometheus và gửi thông báo về  firing alerts đến dịch vụ bên ngoài. 

Xác định các alerting rules:  
Các alerting rules được cấu hình trong Prometheus giống như các recording rules. 

Một tệp quy tắc ví dụ với cảnh báo sẽ là:
```
groups:
- name: example
  rules:
  - alert: HighRequestLatency
    expr: job:request_latency_seconds:mean5m{job="myjob"} > 0.5
    for: 10m
    labels:
      severity: page
    annotations:
      summary: High request latency
```  
#### Templating 
Prometheus hỗ trợ templating trong các chú thích và labels của cảnh báo, cũng như trong các trang bảng điều khiển được cung cấp. Template có khả năng chạy các truy vấn dựa trên cơ sở dữ liệu cục bộ, lặp qua dữ liệu, sử dụng các điều kiện, định dạng dữ liệu, ...  

### Tìm hiểu về PromQL (Operators, Functions... + Example) 

Prometheus cung cấp ngôn ngữ truy vấn được gọi là PromQL( viết tắt bởi Promtheus Query Language) cho phép người dụng select và tổng hợp time series data theo thời gian thực. Kết quả của một biểu thức có thể được hiển thị dưới dạng biểu đồ được xem dưới dạng dữ liệu bảng trên dashboard của Prom hoặc từ các ứng dụng thứ ba thông qua HTTP API.  

***Expression language data types:***  
**Instant vector**: Truy vấn một chuỗi các time series có dùng một timestamp  

VD:
Nếu query http_request_count thì kết quả có dạng như sau:
http_request_count{status=“200”} 20
http_request_count{status=“404”} 3
http_request_count{status=“500”} 5  

**Range Vector**: Truy vấn một chuỗi các time series trong khoảng thời gian

VD:
Nếu query http_request_count[5m] thì kết quả:
http_request_count{status=“200”}
**Scalar**: 1 dấu phảy động đơn giản  

**String** : 1 chuối giá trị đơn giản  

***Literals***  
**String literals**  

Có thể được chỉ định là chuỗi kí tự trong dấu ngoặc kép, ngoặc đơn hoặc or backticks.  
Đối với những kí tự đặc biệt cần thêm dấu . Vd như \n, \t.  

**Float literals**  

Các giá trị float được viết dưới dạng chữ số [-](digits)[.(digits)].  
VD: -2.43  

***Time series Selectors***  

**Instant vector selectors**  
http_requests_total  
Select tất cả time series của metric name http_requests_total  
hoặc  
http_requests_total{job="prometheus",group="canary"}  
Select time series metric name là http_requests_total có job lable là prometheus và group lable là canary   
Ngòai ra ta còn có thể sử dụng các biểu thức chính quy:  
=: Chọn nhãn chính xác so với string khai báo.  
!=: Ngược lại với =  
`=~` : Select lable regex-match với chuỗi khai báo.  
`!~` : Ngược lại với =~  

***Range Vector Selectors***  

Thời lượng được chỉ định là một số được biểu diễn trong [], theo sau là một trong các đơn vị sau:

s - seconds  
m - minutes  
h - hours  
w - weeks  
y - years  
VD select tất cả các giá giá trị trong 5 phút gần đây của tất cả time series metric name http_requests_total và job lable là prometheus  

http_requests_total{job="prometheus"}[5m]  

***Offset modifier***  

Ví dụ: biểu thức sau đây trả về giá trị của http_quests_total 5 phút trong quá khứ so với thời gian truy vấn hiện tại:  

http_requests_total offset 5m  

#### Operators  

Toán tử số học :  
`+ `(phép cộng)  
`- `(phép trừ)  
`* `(phép nhân)  
`/` (phép chia lấy phần nguyên)  
`% `(phép chia lây phần dư))
`^` (lũy thừa)  

Toán tử so sánh:  
`==` (so sánh bằng)  
`!= `(so sánh khác)  
`>` (lớn hơn)  
`< `(nh hơn)  
`>=`(lớn hơn hoặc bằng)  
`<=`(nhỏ hơn hoặc bằng)  

Toán tử logic: and, or, unless  

One to One vector matching: Phương pháp này cố gắng tìm tất cả các cặp phần tử duy nhất từ ​​mỗi vectơ. Các mẫu được chọn hoặc loại bỏ khỏi vectơ kết quả dựa trên các từ khóa “ignoring” và “on”  

Many to one / One to many vector matching: các mẫu được chọn bằng cách sử dụng các từ khóa như “group_left” hoặc “group_right”.  

Toán tử tổng hợp :  
sum (calculate sum over dimensions)
min (select minimum over dimensions)
max (select maximum over dimensions)
avg (calculate the average over dimensions)
group (all values in the resulting vector are 1)
stddev (calculate population standard deviation over dimensions)
stdvar (calculate population standard variance over dimensions)
count (count number of elements in the vector)
count_values (count number of elements with the same value)
bottomk (smallest k elements by sample value)
topk (largest k elements by sample value)

#### Functions  

Trong Prometheus query language, chúng ta có thể sử dụng các hàm được xây dựng sẵn để tạo ra các giá trị mong muốn  
Một số hàm có các đối số mặc định. Ví dụ: `year(v=vector(time()) instant-vector)`.  
Nghĩa là, nếu nó có một đối số `v` nhận giá trị là một instance vector, nếu nó không được cung cấp thì sẽ nhận giá trị của biểu thức `vector(time())`

**abs()**

`abs(v instant-vector)` trả về giá trị tuyệt đối của input

**absent()**

`absent(v instant-vector)` trả về vector rỗng nếu 

**ceil()**

`ceil(v instant-vector)` làm tròn các giá trị của các phần tử `v` lên số nguyên gần nhất

**changes()**

`changes(v range-vector)` trả về số lần giá trị của nó đã thay đổi trong phạm vi thời gian đã cho dưới dạng vectơ tức thời.  

**clamp(), clamp_max(), clamp_min()**  
`clamp(v instant-vector, min scalar, max scalar) ` 
`clamp_max(v instant-vector, max scalar)`
`clamp_min(v instant-vector, min scalar)`  
clamps các giá trị mẫu của tất cả các phần tử trong đó `v` có điều kiện  

**day_of_month()** 

`day_of_month(v=vector(time()) instant-vector)`trả về ngày trong tháng cho mỗi thời điểm nhất định trong UTC. Giá trị trả về là từ 1 đến 31.

**day_of_week()** 

`day_of_week(v=vector(time()) instant-vector)`trả về ngày trong tuần cho từng thời điểm nhất định theo giờ UTC. Các giá trị trả về là từ 0 đến 6, trong đó 0 có nghĩa là Chủ nhật, v.v. 

**days_in_month()** 

`days_in_month(v=vector(time()) instant-vector)`trả về số ngày trong tháng cho mỗi khoảng thời gian nhất định theo giờ UTC. Giá trị trả về là từ 28 đến 31. 

**delta()** 

`delta(v range-vector)`tính toán sự khác biệt giữa giá trị đầu tiên và giá trị cuối cùng của mỗi phần tử time series trong một khoảng v, trả về một vectơ tức thời với các delta đã cho và các labels tương đương. 

VD trả về sự khác biệt về nhiệt độ CPU từ bây giờ đến 2 giờ trước:

`delta(cpu_temp_celsius{host="zeus"}[2h])`  
Notes: delta chỉ nên sử dụng với đồng hồ đo.  

**deriv()** 

`deriv(v range-vector)`tính toán đạo hàm trên giây của time series trong một khoảng v, sử dụng simple linear regression .  
Notes: deriv chỉ nên sử dụng với đồng hồ đo.  

**exp()** 

`exp(v instant-vector)`tính hàm số mũ cho tất cả các phần tử trong v.  
Các trường hợp đặc biệt là:  
Exp(+Inf) = +Inf  
Exp(NaN) = NaN  

**floor()**  

`floor(v instant-vector)`làm tròn xuống các giá trị mẫu của tất cả các phần tử v .  

**histogram_quantile()**  

histogram_quantile(φ scalar, b instant-vector)tính toán lượng tử φ (0 ≤ φ ≤ 1) từ các nhóm bcủa biểu đồ .  

Sử dụng hàm rate() để chỉ định cửa sổ thời gian cho phép tính lượng tử.  

**holt_winters()**  

`holt_winters(v range-vector, sf scalar, tf scalar)`tạo ra một giá trị smoothed cho time series dựa trên khoảng của v. sf và tf nằm trong khoảng từ 0 đến 1.  
Notes:holt_winters chỉ nên sử dụng với đồng hồ đo.  

**hour()**  

`hour(v=vector(time()) instant-vector)`trả về giờ trong ngày cho mỗi thời gian nhất định trong UTC. Giá trị trả về là từ 0 đến 23.

**idelta()**  

`idelta(v range-vector)`tính toán sự khác biệt giữa hai mẫu cuối cùng trong khoảng của v, trả về một vectơ tức thời với các delta đã cho và các labels tương đương.  
Notes: idelta chỉ nên sử dụng với đồng hồ đo.  

**increase()**  

`increase(v range-vector)`tính toán sự gia tăng của chuỗi thời gian trong khoảng v.  

VD trả về số lượng yêu cầu HTTP được đo trong 5 phút qua, trên mỗi time series trong khoảng v :  

`increase(http_requests_total{job="api-server"}[5m])`  
Notes: increasechỉ nên sử dụng với bộ đếm.  

**irate()**  

`irate(v range-vector)`tính toán tốc độ tăng tức thì trên giây của time series trong khoảng v. Điều này dựa trên hai điểm dữ liệu cuối cùng.  

VD trả về tốc độ mỗi giây của các yêu cầu HTTP tìm kiếm trở lại 5 phút cho hai điểm dữ liệu gần đây nhất, trên mỗi chuỗi thời gian trong khoảng v:

`irate(http_requests_total{job="api-server"}[5m])`  
Notes: iratechỉ nên sử dụng khi vẽ đồ thị bộ đếm biến động, chuyển động nhanh.  

**label_join()**  

Đối với mỗi khoảng thời gian trong v, `label_join(v instant-vector, dst_label string, separator string, src_label_1 string, src_label_2 string, ...)` kết hợp tất cả các giá trị của tất cả các thời gian đang `src_labels`sử dụng `separator` và trả về time series với labels `dst_label`chứa giá trị được kết hợp.  

VD:
`label_join(up{job="api-server",src1="a",src2="b",src3="c"}, "foo", ",", "src1", "src2", "src3")`  

**label_replace()**  

Đối với mỗi time series trong v, `label_replace(v instant-vector, dst_label string, replacement string, src_label string, regex string)` đối sánh biểu thức chính quy regex với giá trị của labels `src_label`. Nếu nó khớp, giá trị của labels `dst_label` trong các time series được trả về sẽ là phần mở rộng replacement cùng với các labels ban đầu trong đầu vào.  

VD:  
`label_replace(up{job="api-server",service="a:c"}, "foo", "$1", "service", "(.*):.*")`  

**ln()**  

`ln(v instant-vector)`tính lôgarit tự nhiên cho tất cả các phần tử trong v.  
Các trường hợp đặc biệt là:  
ln(+Inf) = +Inf  
ln(0) = -Inf  
ln(x < 0) = NaN  
ln(NaN) = NaN  

**log2()**  

`log2(v instant-vector)`tính toán lôgarit nhị phân cho tất cả các phần tử trong v.  

**log10()** 

`log10(v instant-vector)`tính toán lôgarit thập phân cho tất cả các phần tử trong v.  

**minute()**  

`minute(v=vector(time()) instant-vector)`trả về phút cho mỗi thời gian nhất định trong UTC. Giá trị trả về là từ 0 đến 59.  

**month()**  

`month(v=vector(time()) instant-vector)`trả về tháng trong năm cho mỗi thời điểm nhất định trong UTC. Các giá trị được trả về là từ 1 đến 12, trong đó 1 có nghĩa là tháng 1,...  

**predict_linear()**  

`predict_linear(v range-vector, t scalar)` dự đoán giá trị của time series t(s) kể từ bây giờ, dựa trên khoảng của v.  
Notes: predict_linear chỉ nên sử dụng với đồng hồ đo.  

**rate()**  

`rate(v range-vector)` tính toán tốc độ tăng trung bình trên giây của chuỗi thời gian trong khoảng v.

VD:  
`rate(http_requests_total{job="api-server"}[5m])`  
Notes: rate chỉ nên sử dụng với bộ đếm. Nó phù hợp nhất để cảnh báo và vẽ đồ thị cho các bộ đếm chuyển động chậm.  

**resets()**  

Đối với mỗi time series đầu vào, `resets(v range-vector)` trả về số lượng bộ đếm được đặt lại trong khoảng thời gian đã cho dưới dạng vectơ tức thời. Bất kỳ sự giảm giá trị nào giữa hai mẫu liên tiếp được hiểu là sự thiết lập lại bộ đếm.  
Notes: resets chỉ nên sử dụng với bộ đếm.  

**round()**  

`round(v instant-vector, to_nearest=1 scalar)` làm tròn các giá trị.  

**scalar()**  

Cho một vectơ đầu vào một phần tử, `scalar(v instant-vector)` trả về giá trị mẫu của phần tử đơn đó dưới dạng một đại lượng vô hướng. Nếu vectơ đầu vào không xác định thì scalar sẽ trả về NaN.  

**sgn()**  

`sgn(v instant-vector)` trả về một vectơ với tất cả các giá trị mẫu được chuyển đổi 1 nếu v dương, -1 nếu v âm và 0 nếu v bằng không.  

**sort()**  

`sort(v instant-vector)` trả về các phần tử vectơ được sắp xếp theo giá trị mẫu của chúng, theo thứ tự tăng dần.  

**sort_desc()**  

Sắp xếp theo thứ tự giảm dần.  

**sqrt()**  
sqrt(v instant-vector)tính căn bậc hai của tất cả các phần tử trong v.

**vector()**  
`vector(s scalar)` trả về scalar s dưới dạng vectơ không có labels.  

**year()**  

`year(v=vector(time()) instant-vector)` trả về năm cho mỗi thời điểm nhất định trong UTC.  

**<aggregation>_over_time()**  

Các hàm sau cho phép tổng hợp từng chuỗi của một vectơ phạm vi nhất định theo thời gian và trả về một vectơ tức thì với kết quả tổng hợp theo từng chuỗi:  
avg_over_time(range-vector): the average value of all points in the specified interval.  
min_over_time(range-vector): the minimum value of all points in the specified interval.  
max_over_time(range-vector): the maximum value of all points in the specified interval.  
sum_over_time(range-vector): the sum of all values in the specified interval.  
count_over_time(range-vector): the count of all values in the specified interval.  
quantile_over_time(scalar, range-vector): the φ-quantile (0 ≤ φ ≤ 1) of the values in the specified interval.  
stddev_over_time(range-vector): the population standard deviation of the values in the specified interval.  
stdvar_over_time(range-vector): the population standard variance of the values in the specified interval.  
last_over_time(range-vector): the most recent point value in specified interval.  
present_over_time(range-vector): the value 1 for any series in the specified interval.  

  
### Tìm hiểu về Labels  
#### Labels là gì và để làm gì?  

Labels: bất kỳ sự kết hợp nhãn đã cho nào cho cùng một metric name xác định particular dimensional instantiation of that metric( Vd: tất cả HTTP requests đã sử dụng phương thức POST tới /api/tracks xử lý) Ngôn ngữ truy vấn cho phép lọc và tổng hợp dựa trên các labels này. Khi thay đổi giá tri label, bao gồm cả thêm hoặc xóa label sẽ tạo ta một time series mới.  
Sử dụng labels để phân biệt các đặc điểm của đối tượng đang được đo:  
`api_http_requests_total `- phân biệt các loại yêu cầu: `operation="create|update|delete"`  
`api_request_duration_seconds` - phân biệt các giai đoạn yêu cầu: `stage="extract|transform|load"`  
Không đặt tên nhãn trong tên chỉ số, vì điều này dẫn đến dư thừa và sẽ gây nhầm lẫn nếu các nhãn tương ứng được tổng hợp lại.  

#### Instrumentation & Target labels 

Phần khả năng về tạo công cụ đo đạc là một lơi thế rất lớn của Prometheus. Prometheus cung cấp khả năng đo đạc (lấy các thông số ) bằng các công cụ xuất trực tiếp (node, database) hoặc các thư viện ngôn ngữ như: Python, go, Ruby ... 

Cách tiếp cận sử dụng Instrumentation 

Khi instument, nên cân nhắc xem là instrument service hoặc libraries (thư viện )

**Service Instumentation:**

online-serving systems: Các dịch vụ có người dùng hoặc service khác đợi phản hồi: web server, databases ..

Thông thường các dịch vụ này thường có các metrics theo nguyên tắc RED ( Request, Error, Duration )
offline-serving systems: Các dịch vụ này không cần phải phản hồi ngay lập tức. Chúng thường tham một hàng đợi công việc: xử lý log . Cho mỗi trạng thái nên có metrics về: lượng công việc trong hàng đợi, công việc đang tiến hành, tốc độ xử lý tiến trình,, lỗi xảy ra. USE method ( Utilisation, Saturation, Error,)

Utilisation: Lượng công việc đang phải xử lý ( processing)
Saturation: Lượng công việc còn lại đang đợi ( waiting )
Error: Lỗi
batch jobs: cũng giống như offline-serving nhưng batch-job chạy theo chu kí còn offline-serving chạy liên tục. Do batch jobs không chạy liên tục nên scrape không hoạt động tốt lắm, nên kỹ thuật nên dùng là Pushgateway. Khi kết thúc batch-jobs nên nên có metrics: how long it took to run ? how long each stage of job took ? time job succeed ? Alert when failed .

**Library instrumentation**

Libraries liên quan tới các mini services: functions, method, cho phép tính toán các thông tin ở mức độ backend

#### Relabel
Relabeling là công cụ mạnh mẽ cho việc tự động viết lại bộ label cho target trước khi nó được scrape. Nhiều bước relabeling có thể được cấu hình với mỗi cấu hình scrape. Chúng áp dụng cho bộ lablel của từng target theo thứ tự xuất hiện của chúng trong file cấu hình.  

### Lưu trữ 
Prometheus lưu trữ dữ liệu lên ổ đĩa local trong cơ sở dữ liệu tùy chỉnh (PromQL) có dạng TSDB(time series database). Độ tin cậy là một thách thức của hệ thống phân tán do đó để duy trì tín tin cậy cao (reliable) Prometheus vẫn chưa hỗ trợ kiến trúc phân tán chính thức. Ngoài ra việc không phân cụm giúp việc chạy các Prometheus dạng binary dễ dàng không phụ thuộc vào các thành phần bên ngoài. Từ lúc phát triển tới nay, cơ chế lưu trữ luôn là phần được chú trong trong Prometheus. Hệ thống lưu trữ được tối ưu để có thể lưu trữ và xử lý hàng triệu mẫu dữ liệu mỗi giây, tương đương hàng chục nghìn exporter trên thực tế, với mỗi mẫu dữ liệu chỉ tốn 1,3 byte. thực tế
#### Các loại lưu trữ Prometheus 

**Local storage**  
Cơ sở dữ liệu chuỗi thời gian địa phương của Prometheus lưu trữ dữ liệu ở định dạng tùy chỉnh, hiệu quả cao trên bộ nhớ cục bộ.  

Remote storage  
Lưu trữ cục bộ của Prometheus được giới hạn ở khả năng mở rộng và độ bền của một nút duy nhất. Thay vì cố gắng giải quyết lưu trữ theo cụm trong chính Prometheus, Prometheus cung cấp một tập hợp các giao diện cho phép tích hợp với các hệ thống lưu trữ từ xa.  

### Tìm hiểu về Alertmanager  

Alerting và Prometheus tách thành 2 phần. Các Alerting rule được Prometheus gửi đến Alertmanager, Alertmanager quản lý việc cảnh báo, bao gồm  silencing, inhibition, aggregation và gửi cảnh báo đi qua các kênh như email, HipChat, PagerDuty. 

3 bước để thiết lập cảnh báo:
- Cài đặt và cấu hình Alertmanager 
- Cấu hình Prometheus liên kết với Alertmanager 
- Tạo các rule alert trong Prometheus

**Alertmanager**  
Alertmanager xử lý cảnh báo được gửi bởi ứng dụng như là Prometheus server. Nó có các cơ chế Grouping, Inhibition, Silience

- Grouping :

Phân loại cảnh báo có những tính chất tương tự. Điều này thực sự hữu ích trong một hệ thống lớn với nhiều thông báo được gửi đông thời. 

Ví dụ: Một hệ thống với nhiều server mất kết nối đến cơ sở dữ liệu, thay vì rất nhiều cảnh báo được gửi về Alertmanager thì Grouping giúp cho việc giảm số lượng cảnh báo trùng lặp, thay vào đó là một cảnh báo để chúng ta có thể biết được chuyện gì đang xảy ra với hệ thống của bạn.

- Inhibition :

Inhibition  là một khái niệm về việc chặn thông báo cho một số cảnh báo nhất định nếu các cảnh báo khác đã được kích hoạt. 

Ví dụ: Một cảnh báo đang kích hoạt, thông báo là cluster không thể truy cập (not reachable). Alertmanager có thể được cấu hình là tắt các cảnh báo khác liên quan đến cluster này nếu cảnh báo đó đang kích hoạt. Điều này lọc bớt những cảnh báo không liên quan đến vấn đề hiện tại. 

- Silience : 

Silience là tắt cảnh báo trong một thời gian nhất định. Nó được cấu hình dựa trên các match, nếu nó match với các điều kiện thì sẽ không có cảnh báo nào được gửi khi đó. 

- High avability:

Alertmanager hỗ trợ cấu hình để tạo một cluster với độ khả dụng cao. 

**Silences Alert**: Tắt cảnh báo trong một thời gian nhất định, cấu hình trên giao diện alertmanager nền web.
Alertmanager được cấu hình với các thông tin như:
Routes: Định tuyến đường đi của notification. Có các route con với các match của nó. Nếu notification trùng với match của route nào đó, thì sẽ được gửi đi theo đường đó. Còn không match với route nào, nó sẽ được gửi theo đường đi mặc định.
Receivers: Cấu hình thông tin các nơi nhận. Ví dụ như tên đăng nhập, mật khẩu, tên mail sẽ gửi đến,....

**Service Discovery**  

Khi các exporter monitor đã được cài đặt, Prometheus cần phải biết các exporter ở đâu ? để tiến hành scrape metrics và có thể thông báo tình trạng sẵn sàng của exporter đó thông qua việc truy vấn tới. Với môi trường mạng ổn định, có thể 1 list danh sách địa chỉ các instance đủ để Prometheus scape dữ liệu. Nhưng với các môi trường mạng động: docker, kubernetes , aws, .. thì cần có service discovery để cung cấp cơ chế cho Prometheus cập nhật thông tin các exporter trong mạng một cách tự động.  

Prometheus có hỗ trợ Service Discovery cho EC2, Kubernetes, Consul, Azure .. hoặc có thể tự tạo custom Service Discovery  
  
## Kết quả thực hành  

### Alert  
<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/alert_1.png"></div>  
  
<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/alert_2.png"></div>  

<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/alert_3.png"></div>  
  
### Memory còn trống dưới 98% và gửi cảnh báo về webhook + gmail  

<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/alertmanager_5.png"></div>  

<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/alertmanager_2.png"></div>  
 
<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/alertmanager.png"></div>  
  
<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/mail.png"></div>  
  
### Metric trên Grafana  

<div style="text-align:center"><img src="https://github.com/vuducthanh0115/Anh/blob/master/Learn%20about%20GIT/node_exporter.png"></div>  
  
### cAdvisor  
  
cAdvisor là 1 dự án Open source của Google mục đích để phân tích mức độ sử dụng, hiệu năng, và rất nhiều thông số khác từ các ứng dụng Container, cung cấp cho người dùng cái nhìn tổng quan về toàn bộ các container đang chạy.  
  
### Node-exporter  
  
Prometheus Node Exporter là một chương trình exporter viết bằng ngôn ngữ Golang. Exporter là một chương trình được sử dụng với mục đích thu thập, chuyển đổi các metric không ở dạng kiểu dữ liệu chuẩn Prometheus sang chuẩn dữ liệu Prometheus. Sau đấy exporter sẽ expose web service api chứa thông tin các metrics hoặc đẩy về Prometheus.  
Node Exporter này sẽ đi thu thập các thông số về máy chủ Linux như : ram, load, cpu, disk, network,…. từ đó tổng hợp và xuất ra kênh truy cập các metrics hệ thống này ở port TCP 9100 để Prometheus đi lấy dữ liệu metric cho việc giám sát.  

