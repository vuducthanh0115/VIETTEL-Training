## Tìm hiểu về docker 

#### Giới thiệu Docker  
Docker là một nền tảng cho phép bạn đóng gói, triển khai và chạy các ứng dụng một cách nhanh chóng. Ứng dụng Docker chạy trong vùng chứa (container) có thể được sử dụng trên bất kỳ hệ thống nào: máy tính xách tay của nhà phát triển, hệ thống trên cơ sở hoặc trong hệ thống đám mây. Và là một công cụ tạo môi trường được "đóng gói" (còn gọi là Container) trên máy tính mà không làm tác động tới môi trường hiện tại của máy, môi trường trong Docker sẽ chạy độc lập.  

Docker được tạo ra để làm việc trên nền tảng Linux , nhưng đã mở rộng để cung cấp hỗ trợ lớn hơn cho các hệ điều hành không phải Linux, bao gồm Microsoft Windows và Apple OS X  

#### Các thành phần cơ bản của Docker  
**Docker Engine**  
Docker Engine là công cụ Client - Server hỗ trợ công nghệ container để xử lý các nhiệm vụ và quy trình công việc liên quan đến việc xây dựng các ứng dụng dựa trên vùng chứa (container). Engine tạo ra một quy trình daemon phía máy chủ lưu trữ images, containers, networks và storage volumes. Daemon cũng cung cấp giao diện dòng lệnh phía máy khách (CLI) cho phép người dùng tương tác với daemon thông qua giao diện lập trình ứng dụng Docker.  

4 đối tượng của Engine là: images, containers, network, volume chúng đều có ID để xác định và phối hợp với nhau để có thể build, ship và run application ở bất cứ đâu  

**Images**: là thành phần để đóng gói ứng dụng và các thành phần mà ứng dụng phụ thuộc để chạy. Và image được lưu trữ ở trên local hoặc trên một Registry (là nơi lưu trữ và cung cấp kho chứa các image)  
**Containers**: là một instance của image, và nó hoạt động như một thư mục, chứa tất cả những thứ cần thiết để chạy một ứng dụng  
**Network**: cung cấp một private network chỉ tồn tại giữa container và host  
**Volume**: Volume trong Docker được dùng để chia sẻ dữ liệu cho container  
#### Docker container  
**Docker Container**  
Một docker container là một môi trường bị tách biệt để đóng gói và chạy ứng dụng. Docker cung cấp một tùy chọn để chạy một ứng dụng trong các container nằm bên cạnh nhau để tăng hiệu quả tính toán. Bạn có thể chạy nhiều container trên cùng một host. Và bạn cũng có thể dễ dàng di chuyển những container này từ host này sang host khác.  
Docker container là một ví dụ của image. Một container chỉ cần kết hợp với các thư viện và thiết lập cần thiết để làm cho ứng dụng hoạt động. Nó là một môi trường đóng gói gọn nhẹ và di động cho một ứng dụng.  

**Cách chạy một docker container**  
Sử dụng lệnh docker để khởi chạy docker container trên hệ thống. Ví dụ lệnh bên dưới sẽ tạo một Docker Container từ image có tên “hello-world”  
```docker run hello-world```  

<img src="https://github.com/vuducthanh0115/Documents/blob/main/test.txt/1_3.png" width="800" height="400" />  

**Liệt kê danh sách docker container**  
Dùng lệnh docker ps để liệt kê các container đang chạy trên hệ thống hiện tại. Nó sẽ không liệt kê các container bị dừng. Nó sẽ hiển thị Container ID, name và các thông tin khác về container.  
```docker ps```  

<img src="https://github.com/vuducthanh0115/Documents/blob/main/test.txt/2_3.png" width="800" height="400" />  

Dùng tùy chọn -a với lệnh ở trên để liệt kê tất cả các container bao gồm cả container bị dừng.  
docker ps -a  

<img src="https://github.com/vuducthanh0115/Documents/blob/main/test.txt/3_3.png" width="800" height="400" />  

Tìm kiếm tất cả thông tin chi tiết về container  
```docker inspect <ID container>```  

Xóa Docker container
Dùng lệnh docker rm để xóa docker container đang tồn tại. Bạn cần cung cấp docker container id hoặc container name để xóa một container cụ thể.  
```docker stop <ID container>```  

```docker rm <ID container>```  

**Lưu container thành images**  
Ta sử dụng lệnh : docker commit <containeri ID>  

<img src="https://github.com/vuducthanh0115/Documents/blob/main/test.txt/4_3.png" width="800" height="400" />  

#### Cơ chế lưu trữ của docker  

Cơ chế lưu trữ copy-on-write  
Tạo 1 hệ thống mới ngay lập tức mà không cần copy tất cả file hệ thống  
Hệ thống lưu trữ lưu lại mỗi thay đổi  


**Chạy các tiến trình trong docker contaier**  

**docker run**  
Khởi tại 1 container bằng cách truyền vào tên 1 images và 1 tiến trình để yêu cầu chạy trong container.  
Container có tiến trình chính
Container dừng khi tiến trình chính kết thúc  
Container có thể được đặt tên  

**docker attach**  
Truy cập container đang chạy thông qua ID hoặc tên  
Có thể truy cập vào cùng 1 container từ nhiều nơi tại cùng 1 thời điểm  
Ctrl-p/Ctrl-Q để ra khỏi container và vẫn để tiến trình chạy  

**docker exec**  
Khỏi tại 1 process khác bên trong container đã có  
Tiện lợi cho việc debug và quản lí database  
Không thể thêm port, volume, ...  

**Một số lệnh thường dùng với container**  

**docker create**  
Tạo ra 1 container với các config tương tự docker run  
Container không được chạy ngay từ đầu  
Dùng lệnh docker start để chạy container  
Cú pháp: docker create [options] images [command][arg...]
<img src="https://github.com/vuducthanh0115/Documents/blob/main/test.txt/5_3.png" width="800" height="400" />  

**docker start/stop/restart**  
Thay đổi trạng thái cảu container, từ running sang stopped hoặc khởi động lại container  
Stop :  
-  Gửi tín hiệu SIGTERM để yêu cầu tắt tiến trình  
-  Gửi tín hiệu SIGKILL nếu chưa tắt sau 1 khoảng thời gian nhất định  
Cú pháp: docker start/stop/restart [options] container [container]  
<img src="https://github.com/vuducthanh0115/Documents/blob/main/test.txt/6_3.png" width="800" height="400" />  

**docker cp**  
Copy dữ liệu (file/filder) từ container tới local machine và ngược lại  
Áp dụng cho tất cả stopped và running container  
Đường dẫn relative  
Cú pháp: docker cp [options] container:src_path dest_path  

**docker inspect**  
Kiểm tra các thiết lập của Docker (network, driver, ...)  
In ra các thông tin dưới dạng JSON  
Cú pháp: docker inspect [options] container|image|task [container|image|task...]  

**docker rm**  
Xóa container dựa theo name hoặc ID  
Cần stop container trước khi xóa bỏ  
Cú pháp: docker rm [options] container [container...]  

**docker logs**  
Xem output của container  
docker logs [option] container  
Không nên để cho dung lượng log quá lớn  

**docker kill**  
Dừng container  
docker kill [option] container [container...]  

**docker run --memory <total-memory-limit><image><command>**  
Giới hạn tài nguyên  

**docker run --cpu-shares=<limit><image><command>**  
Giới hạn CPU  tương đối  

#### Mạng nội b trong container  

Các chương trình trong container được mặc định tách biệt hoàn toàn khỏi Internet  
Nhóm các container lại thành 1 mạng nội bộ  
Kiểm soát sự liên kết giữa các container này với container kia  
Sử dụng phương pháp expose cổng và link container  
Docker có cơ chế đặc biệt giúp container tìm và liên kết với nhau  
Xác định cổng bên trong và bên ngoài container  
Không giới hạn số lượng cổng để mở  

**Mở cổng container**  

Cần sự phối hợp giữa các container  
Dễ dàng tìm kiếm cổng được mở  
Cổng bên trong container là cố định  
Cổng bên ngoài container được lựa chọn ngẫu nhiên  
Cho phép nhiều container chạy các chương trình với cổng cố định  
Thường được sử dụng với các chương trình tìm kiếm dịch vụ  

**Liên kết giữa các container**  

Liên kết tr tiếp các container  
-  Dùng để kiểm tra xem container đang chạy gì và ở chỗ nào  
-  Kết nối tất cả các cổng, nhưng 1 chiều  
-  Chỉ dành cho các dịch vụ mà không thể chạy trên nhiều máy khác nhau  
-  Tự động gán hostname  
-  Liên kết có thể bị đứt nếu container khởi động lại  

Liên kết động giữa các container  
-  Docker cung cấp tính năng tạo mạng riêng nội bộ  
-  Name server với cơ chế quản lý địa chỉ IP và name  
-  Cần tạo lập mạng trước rồi chạy các container liên quan   
-  Lập mạng riêng : docker network create [option] network  

#### Cách cài đặt docker  

Bước 1: Update các package và cài các package cần thiết  
```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
```  

Bước 2: Thêm Docker’s official GPG key:  
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```  

Bước 3: Thêm Docker Repository   
```
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```  

Bước 4: Cài đặt docker  
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```  

Bước 5: Kiểm tra  
```
sudo docker run hello-world
```  

#### Các câu lệnh cơ bản  

***Docker tag***  
Gắn tag cho TARGET_IMAGE tương ứng với SOURCE_IMAGE.  
```
 docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```
***Docker run***  
Đây là câu lệnh dùng để khởi tạo một container dựa vào Image có sẵn, cú pháp:  
```
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```
Option  
--name cho phép đặt tên container.  
-t cung cấp một giao diện để gõ command bên trong container.  
-i giúp cho các chương trình bên trong container nhận được những command đã viết.  

***Docker build***  
Thực hiện lệnh trong thư mục chứa file Dockerfile  
docker build [OPTIONS] PATH | URL | -  

***Docker push***  
Đẩy image, repository lên Docker HUB.  
docker push [OPTIONS] NAME[:TAG]  

***Docker pull***  
Pull một image hoặc repository từ Docker HUB đăng ký.
docker pull [OPTIONS] NAME[:TAG|@DIGEST]  

**Docker CE/Docker EE**  
Docker Community Edition (CE): Là phiên bản miễn phí và chủ yếu dựa vào các sản phầm nguồn mở khác.  
Docker Enterprise(EE): Khi sử dụng phiên bản này bạn sẽ nhận được sự support của nhà phát hành, có thêm các tính năng quản lý và security.   

**Docker Compose**  
Docker compose là công cụ dùng để định nghĩa và run multi-container cho Docker application. Với compose sử dụng file YAML để config các services cho application. Sau đó dùng command để create và run từ những config đó.  
Docker compose cho phép tạo nhiều service(container) giống nhau bằng lệnh :
$ docker-compose scale <tên service> = <số lượng>  
Sử dụng chỉ với ba bước:  
Khai báo app’s environment trong Dockerfile.  
Khai báo các services cần thiết để chạy application trong file docker-compose.yml.  
Run docker-compose up để start và run app.  
Cú pháp :  
- Tạo file docker-compose.yml  
- Viết theo cú pháp của ngôn ngữ yaml  
- Viết theo đúng cú pháp cảu từng version cảu docker-compose  

Các lệnh trong docker compose :  
- version: chỉ ra phiên bản docker-compose đã sử dụng  
- services: thiết lập các services(containers) muốn cài đặt và chạy  
- image: chỉ ra image được sử dụng trong lúc tạo container  
- build: dùng để tạo container  
- port: thiết lập ports chạy tại máy host và trong container  
- restart: tự động khởi chạy container bị tắt  
- environment: thiết lập biến môi trường  
- depends_on: chỉ ra sự phụ thuộc. Tức là service nào phải dduwwocj cài đặt và chạy trước thì service dduwwocj config tại đói mới được chạy  
- volumes: dùng để mount 2 thư mục trên host và container với nhau  
- links: Cho phép đăng kí 1 cái tên(bí danh) để cho các Server khác có thể gọi nó  
- context: Xác định thư mục chứa gốc, dựa vào thư mục này chúng ta sẽ khai báo tiếp đường dẫn dockerfile   
**Docker Registry**  
Docker Registry là một dịch vụ máy chủ cho phép lưu trữ các docker image của cá nhân, công ty, team,… Dịch vụ Docker Registry có thể được cung cấp bởi tổ chức thứ 3 hoặc là dịch vụ nội bộ được xây dựng riêng nếu bạn muốn. Một số dịch vụ Docker Registry phổ biến như :  
- Azure Container Registry  
- Docker Hub  
- Quay Enterprise  
- Google Container Registry.  
- AWS Container Registry  

<img src="https://github.com/vuducthanh0115/Documents/blob/main/test.txt/7_3.png" width="800" height="400" />  

**Docker Daemon**  
Docker Daemon: là server Docker cho yêu cầu từ Docker API. Nó quản lý images, containers, networks và volume.  

**Docker volume**  
Là 1 nơi lưu trữ data nằm ngoài container, mục đích không làm mất data khi xóa container  
Sử dụng volume khi :  
- Khi chia sẻ dữ liệu giữa nhiều container đang chạy  
- Lưu dữ liệu tới 1 server remote hoặc cloud  
- Khi cần backup, restore hoặc migrate dữ liệu từ Docker Host này sang Docker Host khác  

Lệnh volume:  
- docker volume create: Tạo mạng mới  
- docker volume inspect: Xem chi tiết mạng  
- docker volume ls: Hiện thị những mạng đã có  
- docker volume rm: Xóa mạng  
- docker volume prune: Xóa các volume rỗng  

**Docker network**  
Để kết nối các container trong cùng 1 mạng hoặc khác mạng với nhau.  
Các câu lệnh thao tác với mạng  
- ocker network create: Tạo mạng mới  
- docker network inspect: Xe, chi tiết mạng  
- docker network ls: Hiện thị những mạng đã có  
- docker network rm: Xóa mạng  
- docker network prune: Xóa đông loạt các mạng không sử dụng  
- docker network connect: Tạo kết nối mạng  
- docker network disconnect: Ngắt kết nối mạng  








