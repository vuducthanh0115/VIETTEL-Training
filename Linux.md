# Tổng quan về Linux  
**Sự khác biệt của Linux với Windows**  
***Về lịch sử phát triển:***  
+  Linux miễn phí và là mã nguồn mở ngay từ khi mới ra đời năm 1991. Linux bắt đầu như một dự án, nhưng nó đã nhanh chóng trở thành một trong những dự án mã nguồn mở lớn nhất từ trước đến nay.  
+  Còn đối với Windows, phiên bản Windows 1.0 của Microsoft được phát hành vào năm 1985 và không giống như Linux, nó là một sản phẩm mã nguồn đóng hoàn toàn được Microsoft bán theo chương trình cấp phép.  
***Về xử lý, can thiệp vào mã nguồn:***  
+  Có thể chỉnh sửa, thay đổi các tính năng đối với Linux, nhưng với Windows thì không.  
+  Linux được cấp phép GNU Public License nên nó cho phép người dùng truy cập mã nguồn đến tận lõi của hệ điều hành.Còn đối với hệ điều hành Windows thì không, chỉ trừ khi là kỹ sư trong nhóm phát triển hệ điều hành Windows, còn không thì không có quyền truy cập vào mã nguồn này. Nó được bảo mật vô cùng cẩn thận.    
***Về vấn đề bản quyền:***  
+  Để có quyền truy cập mã nguồn Linux thì phải được cấp phép. Cấp phép nghĩa là phần mềm sẽ có quyền được phân phối. Với giấy phép GPL của Linux, bạn có thể tự do sửa đổi OS đó, tái xuất bản nó và thậm chí bạn có thể thương mại nó, miễn là bạn cung cấp mã nguồn của nó, không giữ bí mật cho riêng mình.Với giấy phép GPL, bạn cũng có thể tải xuống bản sao của Linux và cài đặt nó trên bao nhiêu máy tùy ý.  
+  Còn giấy phép của Microsoft thì sẽ rất khác với giấy phép này, tức là bạn không thể sửa đổi mã nguồn vì Microsoft không bao giờ công bố mã nguồn của hệ điều hành này.  
+  Khi bạn  mua bản quyền Windows (đối với các cá nhân) thì chỉ sử dụng giấy phép đó cho cho một máy tính duy nhất. Còn các giấy phép dành cho máy doanh nghiệp thì khác,có thể sử dụng 1 key để kích hoạt cho nhiều máy tính.  
***Về ứng dụng – phần mềm:***  
+  Với hầu hết các bản phối của hệ điều hành Linux,có một trung tâm để cài đặt các ứng dụng. Điều này giúp dễ dàng thêm các ứng dụng mới và xóa chúng đi khi không còn dùng đến.Tính năng quản lý gói của Linux cực kỳ hữu ích vì có thể tìm kiếm và cài đặt ứng dụng trực tiếp mà không cần phải dò tìm trên mạng. Và tất cả đều miễn phí.Trước đây, Windows không có kho ứng dụng của riêng mình. Với Windows, bạn phải lên Google và tìm kiếm những phần mềm của bên thứ 3 để cài đặt.Sau đó đến quá trình tải về máy rồi chạy file thực thi .exe để tiến hành cài đặt. Sau khi ứng dụng đã được cài đặt,cũng không biết nó đã thay đổi bao nhiêu tập tin hệ thống. Nhưng kể từ phiên bản Windows 8.x, Microsoft đã có kho ứng dụng riêng của mình – nó mang tên Windows Store, mặc dù còn hạn chế so với Linux nhưng nó cũng cung cấp khá nhiều phần mềm (cả miễn phí và trả phí), đáp ứng nhu cầu cơ bản của người dùng.  
***Về khả năng sử dụng:***  
+  Linux rất phức tạp để cài đặt nhưng có khả năng hoàn thành các tác vụ phức tạp dễ dàng hơn.  
+  Windows cung cấp cho người dùng một hệ thống đơn giản để vận hành nhưng sẽ mất nhiều thời gian hơn để cài đặt.  
***Về đối tượng sử dụng***  
***Về bảo mật:*** Cả 2 đều có tính bảo mật nhưng linux có tính bảo mật cao hơn.  
***Về khả năng hỗ trợ:*** Windows là một sản phẩm thương mại hoàn toàn nên về khâu support sẽ tốt hơn.  
***Về cập nhật:***  
+  Linux, người dùng có toàn quyền kiểm soát các bản cập nhật, chúng tôi có thể cài đặt bất cứ khi nào chúng tôi cần và sẽ mất ít thời gian hơn mà không cần khởi động lại.
+  Windows, các bản cập nhật sẽ đến vào những thời điểm bất tiện như bạn đang in một bản in cho máy in nhưng đột nhiên bản cập nhật bật lên sẽ khiến người dùng bực bội và mất nhiều thời gian hơn để cài đặt.  

### Tổng quan  
#### Kiến trúc  
Kiến trúc hệ điều hành Linux chia làm 3 phần:  
- Kernel  
- Shell  
- Applications  
#### Thành phần  
- **Kernel** : Đây là phần quan trọng của HĐH, phần kernel chứa các module, thư viện để quản lý và giao tiếp với phần cứng và các ứng dụng.  
Dùng để quản lý phần cứng và các ứng dụng thực thi  
  + Linux xem mỗi thiết bị phần cứng tương đương với một tập tin  
  + Khi khởi động máy tính, Kernel được nạp vào trong bộ nhớ chính, và nó hoạt động cho đến khi tắt máy. Thực hiện chức năng mức thấp và chức năng mức hệ thống.  
  + Kernel chịu trách nhiệm thông dịch và gửi các chỉ thị tới bộ vi xử lý máy tính.  
  + Kernel cũng chịu trách nhiệm về các tiến trình và cung cấp các đầu vào và ra cho các tiến trình.  
- **Shell**: là một chương trình có chức năng thực thi các lệnh từ người dùng hoặc từ các ứng dụng – tiện ích yêu cầu chuyển đến cho Kernel xử lý.  
***Các loại shell:***  
  + Sh (the Bourne Shell)  
  + Bash(Bourne-again shell): đây là shell mặc định trên linux.
  + csh (the C shell): shell được viết bằng ngôn ngữ lập trình C.  
  + ash (the Almquist shell).  
  + tsh (the TENEX C shell).  
  + zsh (the Z shell).  

***Chức năng của Shell:***  
  + Thông dịch lệnh.  
  + Khởi tạo chương trình.  
  + Định hướng vào ra.  
  + Kết nối đường ống.  
  + Thao tác trên tập tin.  
  + Duy trì các biến.  
  + Điều khiển môi trường.  
  + Lập trình shell.  

- **Applications**: Là các ứng dụng và tiện ích mà người dùng cài đặt trên Server. Ví dụ: ftp, samba, Proxy, …  

- **Commands and Utilities**: 
Khi làm việc với HĐH Linux hầu như tất cả người dùng đều sử dụng lệnh để làm việc. Lệnh là một chương trình hoặc một script dùng để thực thi một nhiệm vụ nào đó. Lệnh được gõ sau dấu nhắc shell.  
Dòng lệnh shell tổng quát có dạng như sau: command [options]  
Trong đó:  
  + command Lệnh  
  + options Tùy chọn, thường bắt đầu bằng - hoặc - -.Nhiều tùy chọn có thể kết hợp bằng một ký hiệu -. Ví dụ: -lF thay vì -l -F  

Dòng lệnh shell có phân biệt chữ thường và chữ hoa.  

***Các lệnh cơ bản :***  

**1. Lệnh trợ giúp: man**  
Mỗi lệnh trên Linux có rất nhiều options, mỗi options thực hiện các chức năng khác nhau, người quản trị cũng không cần nhớ hết các options của lệnh mà chỉ cần nhớ một vài options thông dụng. Để biết một lệnh có bao nhiêu options cũng như chức năng của từng options thì lệnh đầu tiên cần phải biết là lệnh: man  
Cấu trúc lệnh: ```$ man <tên lệnh>```  
Ví dụ: Để xem hướng dẫn sử dụng lệnh cp (copy) có thể nhập lệnh $man cp  
Để thoát khỏi man ta bấm phím “q”  
<img src="https://github.com/vuducthanh0115/img/blob/main/anh/1_2.png" width="800" height="400" />  

**2. Các lệnh kiểm tra performance**  
Lệnh xem thông tin RAM: Xem tổng dung lượng, dung lượng hiện tại đang dùng, dung lượng còn trống. có 2 lệnh đó là:  
- cat /proc/meminfo  
Lệnh cat: Dùng để đọc nội dung của file text  
```/proc/meminfo```: đây là đường dẫn (đường dẫn tuyệt đối) tới file chứa thông tin RAM có tên là meminfo  
- free  
các options:  
  - -b Hiển thị theo bytes  
  - -k Hiển thị theo kilobytes  
  - -m Hiển thị theo megabytes  
  - -g Hiển thị theo gigabytes  
  - --tera Hiển thị theo terabytes  
  - -h Hiển thị theo kiểu tự động gom theo khối dữ liệu  

Lệnh xem thông tin CPU: cat /proc/cpuinfo  
Lệnh hiển thị thông tin kernel: ```uname -a```  
options:  
-a : all information  
Lệnh hiển thị phiên bản: ```cat /etc/redhat-release```  
Lệnh xem dung lượng ổ cứng: Xem dung lượng ổ cứng đã dùng và còn trống bao nhiêu: ```df-h```  
options: 
 -h : in kích thước mà người dùng có thể đọc  
Lệnh xem các tiến trình: top  
Lệnh xem dung lượng của thư mục: du  
options:  
- -s : xuất kết quả theo summarize (tổng dung lượng)  
- -h: in kích thước mà người dùng có thể đọc  

Ví dụ: Xem dung lượng của thư mục /etc  
 du -sh /etc  
Lệnh xem tên server: hostname  
Lệnh xem địa chỉ ip: ifconfig  

#### Files and Directories  
Trên linux tất cả mọi thứ đều được xem dưới dạng là file. Có 3 loại file: file thông thường (Regular files), file thư mục (Directory files), file đặc biệt (Special files).  
File thông thường: một chương trình, file text, library, file nhạc …  
Thư mục: thành phần dùng để chứa các file khác (container).  
File đặc biệt: (device, socket, pipe, symbolic links …).  
- -: Regular file  
- d: Directory  
- l: Link  
- c: Special File  
- s: Socket  
- p: Named Pipe  
- b: Block Device  
Các file ẩn thường bắt đầu bằng dấu “.”  

Cấu trúc hệ thống file được bố trí theo dạng hình cây(tree) :  
<img src="https://github.com/vuducthanh0115/img/blob/main/anh/2_2.png" width="800" height="400" />  
Bắt đầu là thư mục gốc “/”, sau đó là các thư mục con (hay còn gọi là nhánh): /bin, /sbin, /home, /mnt …  
Mỗi thư mục con của thư mục gốc có các chức năng khác nhau.  
/bin: Chứa các file binary của các tập lệnh trong Linux.  
/sbin: Tương tự như /bin, nhưng là những lệnh chỉ được dùng bởi quản trị hệ thống - tương đương root user.  
/boot: Chứa các thư viện cần thiết cho quá trình khởi động.  
/dev: Chứa thông tin chứa các file thiết bị. Trong Linux, mỗi thiết bị đều có file đại diện và được đặt tên theo 1 Logic nhất định:  
- cdrom : đĩa CDRom / DVD  
- fd* : Đĩa mềm  
- hd* : Đĩa cứng IDE  
- sd* : Đĩa cứng SCSI  
- st* : Băng từ  
- tty* : cổng giao tiếp (COM,...)  
- eth* : card ethenet  

/etc: Chứa file cấu hình hệ thống và ứng dụng.  
/lib: Chứa thư viện chia sẻ được dùng bởi các tiến trình, các lệnh boot, lệnh hệ thống như trong /bin và /sbin.  
/lib64: Tương như như lib nhưng dành cho 64bit.  
/opt: Nơi dành riêng cho các tiện ích chương trình được cài đặt.  
/media: Thư mục có vai trò như đích đến của quá trình mount point. Khi gắn 1 thiết bị lưu trữ bên ngoài, để sử dụng, cần mount thiết bị này vào /media, từ đó, các thư mục, tập tin sẽ được chuyển vào đây (lúc này /media có thể coi như ảnh chiếu của thiết bị).  
/run:  
/root: Thư mục home của user root.  
/home: Thư mục chứa các thư mục home của các user được tạo.  
/sys:  
/srv : chứa dữ liệu, các file của các dịch vụ trên hệ thống.  
/mnt: Thư mục này được dùng để gắn các hệ thống tập tin tạm thời (mounted filesystems).  
/proc: Lưu các thông tin về tình trạng của hệ thống.  

#### Quản lý thư mục, Quản lý tập tin  
Lệnh ls: dùng để xem (liệt kê) nội dung thư mục  
Cấu trúc lệnh: ```ls [options] [Path]```  
Options:  
  -  -l: liệt kê chi tiết.  
  -  -a: liệt kê tất cả các file ẩn   
  -  -t: liệt kê các file được sắp xếp theo ngày sửa đổi  
  -  -r: liệt kê các dile theo kiểu đảo ngược lại  
  -  -i: liệt kê số node của các file  

<img src="https://github.com/vuducthanh0115/img/blob/main/anh/3_2.png" width="800" height="400" />  

cd
Lệnh cd: dùng để chuyển thư mục  
Cấu trúc lệnh: ```cd[Path]```  
Ví dụ: cd /etc Chuyển đến thư mục /etc.  
cd usr Chuyển vào thư mục usr là con của thư mục hiện tại.  
cd .. Chuyển lên thư mục cấp cao hơn (cha)  
cd Chuyển về thư mục home  
cd ~ Chuyển về thư mục home  

Lệnh pwd: cho biết thư mục làm việc hiện tại.  
Cấu trúc lệnh: ```$ pwd```  

Lệnh passwd: đổi mật khẩu đăng nhập của user đang login.  
Cấu trúc lệnh: ```$ passwd```  

Lệnh cp: dùng để sao chép file  
Cấu trúc lệnh: ```cp [Options] Source Dest```  
Options:  
-R, -r : Sao chép toàn bộ thư mục.  
Source, Dest: Lần lượt là tên thư mục/tập tin nguồn, đích  

Lệnh mv: dùng để đổi tên / di chuyển thư mục hoặc file từ nơi này sang nơi khác  
Cấu trúc lệnh: ```mv [options] Source Dest```  
Options:  
-i : Nhắc trước khi di chuyển với tập tin/thư mục đích đã có rồi.  
-f: Ghi đè khi di chuyển với tập tin/thư mục đích đã có rồi.  

Lệnh mkdir: dùng để tạo thư mục  
Cấu trúc lệnh: ```mkdir [Options] Directory```  
Options:  
-p : Cho phép tạo thư mục con ngay cả khi chưa có thư mục cha.  
Directory: Tên thư mục muốn tạo.  

Lệnh rmdir: dùng để xóa thư mục rỗng. Thư mục rỗng là thư mục không chứa bất kỳ
thành phần nào.  
Cấu trúc lệnh: ```rmdir [options] directory```  
Options:  
-p : xóa thư mục và cả thư mục cha.  
Directory: Tên thư mục muốn xóa.  

Lệnh rm: dùng để xoá file/thư mục. Lệnh này được xem là một trong những lệnh nguy hiểm của Linux.  
Cấu trúc lệnh: ```rm [options] file```  
Options:  
-f: xóa không cần hỏi  
-i: hỏi trước khi xóa  
-R, -r: xóa toàn bộ thư mục, kể cả thư mục con  

Lệnh gedit: dùng để mở file với trình soạn thảo gedit.  

Lệnh vi: dùng để mở trình soạn thảo thảo vi.  

#### Vim & Nano Editor:  
Là trình soan thảo Terminal  

***GNU nano***  
GNU nano là một trình soạn thảo văn bản dòng lệnh dễ sử dụng cho các hệ điều hành Unix và Linux. Nó bao gồm tất cả các chức năng cơ bản của một trình soạn thảo văn bản thông thường, như Syntax Highlighting, bộ đệm, tìm kiếm và thay thế văn bản, kiểm tra chính tả, mã hóa UTF-8,...  
Cài đặt Nano trên Ubuntu  
```sudo apt install nano -y```  
Các tính năng của GNU nano bao gồm:  
+ Hỗ trợ Autoconf  
+ Chức năng tìm kiếm phân biệt chữ hoa chữ thường  
+ Tìm kiếm và thay thế tương tác  
+ Khả năng tự động thụt lề  
+ Tùy chọn chiều rộng tab được hiển thị  
+ Tìm kiếm và thay thế biểu thức thông thường  
+ Công tắc chuyển đổi cho flag cmdline thông qua các phím meta  
+ Tab completion (nhấn Tab trong khi nhập lệnh, tùy chọn hoặc tên file và môi trường shell sẽ tự động hoàn thành những gì bạn đang nhập) khi đọc/ghi file  
+ Soft text wrapping (văn bản trông giống như đã kết thúc ở phần rìa màn hình, nhưng thực tế, nó là một dòng rất dài. Các phần tiếp theo được chỉ định bằng $)  
<img src="https://github.com/vuducthanh0115/img/blob/main/anh/5_2.png" width="800" height="400" />  
<img src="https://github.com/vuducthanh0115/img/blob/main/anh/6_2.png" width="800" height="400" />  

***Vim***  
Vim - viết tắt của từ Vi IMproved là một bản sao, với một số bổ sung, của trình soạn thảo vi của Bill Joy cho Unix. Nó được viết bởi Bram Moolenaar dựa trên mã nguồn của một port của Stevie editor lên Amiga và phát hành lần đầu vào năm 1991. Vim được sử dụng rất mạnh mẽ trong CLI (command-line interface). Linux sử dụng rất nhiều file cấu hình, mình thường sẽ cần chỉnh sửa chúng và vim là một công cụ để làm điều đó.  
Cài đặt Vim trên linux  
```sudo apt-get install vim```  
Vim có lợi thế là mạnh hơn GNU nano. Vim không chỉ chứa nhiều tính năng hơn, mà bạn còn có thể tùy chỉnh chương trình với các plugin và script.  
Các tính năng của Vim bao gồm:  
+ Các lệnh tự động  
+ Các lệnh bổ sung  
+ Đầu vào  
+ Giới hạn bộ nhớ cao hơn vanilla vi  
+ Chia nhỏ màn hình  
+ Khôi phục phiên  
+ Mở rộng tab  
+ Hệ thống tag  
+ Thêm màu cho cú pháp  

<img src="https://github.com/vuducthanh0115/img/blob/main/anh/4_2.png" width="800" height="400" />  

**Các biến môi trường**  
Biến môi trường là các đại lượng có các giá trị cụ thể. Một số biến môi trường được cung cấp các giá trị đặt trước của hệ thống và các biến khác được đặt trực tiếp bởi người dùng, tại dòng lệnh hoặc trong khi khởi động các tập lệnh khác.  
Biến môi trường là một chuỗi ký tự chứa thông tin được sử dụng bởi một hoặc nhiều ứng dụng.  
Một số lệnh có sẵn cho phép liệt kê và đặt các biến môi trường trong Linux:  
-  env – Lệnh cho phép bạn chạy một chương trình khác trong môi trường tùy chỉnh mà không cần sửa đổi chương trình hiện tại. Khi được sử dụng mà không có đối số, nó sẽ in một danh sách các biến môi trường hiện tại.  
-  printenv – Lệnh in tất cả hoặc các biến môi trường được chỉ định.  
-  set– Lệnh dùng để set hoặc unset biến shell. Khi được sử dụng mà không có đối số, nó sẽ in một danh sách tất cả các biến bao gồm các biến môi trường và shell và các hàm shell.  
-  unset – Lệnh xóa các biến shell và môi trường.
-  export – Lệnh đặt các biến môi trường.  
Một số biến môi trường phổ biến nhất:  
-  USER – Người dùng đăng nhập hiện tại.  
-  HOME – Thư mục home của người dùng hiện tại.  
-  EDITOR– Trình chỉnh sửa tập tin mặc định sẽ được sử dụng. Đây là trình chỉnh sửa sẽ được sử dụng khi bạn nhập edit vào terminal của bạn.  
-  SHELL – Đường dẫn của shell hiện tại của người dùng, chẳng hạn như bash hoặc zsh.  
-  LOGNAME – Tên của người dùng hiện tại.  
-  PATH– Một danh sách các thư mục sẽ được tìm kiếm khi thực hiện các lệnh. Khi bạn chạy một lệnh, hệ thống sẽ tìm kiếm các thư mục theo thứ tự này và sử dụng tệp thực thi đầu tiên được tìm thấy.  
-  LANG – Các cài đặt local hiện tại.  
-  TERM – Terminal emulation hiện tại.  
-  MAIL – Vị trí lưu trữ thư của người dùng hiện tại.  

**Quản lý tiến trình**  
Tiến trình - process là một khái niệm cơ bản trong bất kì một hệ điều hành nào. Một tiến trình có thể được định nghĩa là một thực thể chương trình đang được chạy trong hệ thống.  
VD mở 5 chương trình vim để thao tác với 5 file khác nhau, thì cho 5 tiến trình chạy trong hệ thống.  
--> Tiến trình là một thực thể chương trình đang được thực thi. Nó là một tập hợp các cấu trúc dữ liệu mô tả đầy đủ quá trình một chương trình được chạy trong hệ thống.  
Để có thể quản lý một tiến trình, kernel cần phải biết được tiến trình đó đang làm những gì. Ví dụ, kernel cần phải biết mức độ ưu tiên của tiến trình – biết tiến trình đang chạy (sử dụng CPU) hay đang bị blocked – khóa để chờ một sự kiện nào đó. Kernel cũng cần biết không gian địa chỉ nào đang được tiến trình đó sử dụng, những file nào mà tiến trình được truy cập …  

Trạng thái của tiến trình  
TASK_RUNNING – Trạng thái đang chạy  
Tiến trình đang được thực thi (đang sử dụng CPU) hoặc đang chờ được thực thi (chờ để được lập lịch thực hiện).  
TASK_INTERRUPTIBLE – Trạng thái có thể làm gián đoạn  
Tiến trình đang được tạm dừng (đang ngủ) để chờ một số điều kiện xảy ra để thực thi tiếp. Một ngắt phần cứng được tạo ra (hardware interupt), hoặc sự giải phóng một tài nguyên hệ thống mà tiến trình đang chờ đợi để được sử dụng, hoặc chờ một tín hiệu – signal là những ví dụ về những điều kiện có thể đánh thức một tiến trình đang tạm dừng. Việc “đảnh thức” sẽ thực hiện hành động chuyển trạng thái tiến trình từ TASK_INTERRUPTIBLE sang TASK_RUNNING.  
TASK_UNINTERRUPTIBLE – Trạng thái không thể làm gián đoạn  
Trạng thái này giống trạng thái TASK_INTERRUPTIBLE, trừ việc tiến trình trong trạng thái này không thể chuyển trạng thái khi nhận được signal. Trạng thái này hiếm khi được sử dụng, thường thì sẽ sử dụng trạng thái TASK_INTERRUPTIBLE. TASK_UNINTERRUPTIBLE được sử dụng trong vài điều kiện đặc trưng của tiến trình, khi tiến trình đang đợi một sự kiện gì đó mà không muốn bị ngắt, bị gián đoạn.  
TASK_STOPPED – Trạng thái dừng  
Tiến trình sẽ chuyển sang trạng thái dừng nếu nhận được một trong các tín hiệu – signal: SIGSTOP, SIGTSTP, SIGTTIN, hoặc SIGTTOU.  
TASK_TRACED – Trạng thái truy tìm  
Tiến trình đang thực thi thì bị dừng lại bởi một công cụ tìm lỗi – debugger. Một công cụ tìm lỗi thực hiện ptrace() system call để theo dõi một chương trình test, nó sẽ gửi các signal cho chương trình test đó, và trạng thái của chương trình test sẽ chuyển sang TASK_TRACED.  
Tóm lại, trạng thái TASK_TRACED được sử dụng khi các công cụ tìm lỗi muốn đặt các điểm debug, muốn dừng chương trình test lại để thay đổi giá trị đầu vào …  
EXIT_ZOMBIE – Trạng thái zombie  
Điều kiện để một tiến trình chuyển sang trạng thái EXIT_ZOMBIE là:  
Nó là tiến trình con  
Nó kết thúc khi tiến trình cha của nó vẫn đang được thực thi  
Tiến trình cha không gọi wait4() system call  
Với những điều kiện trên, khi tiến trình con kết thúc, tài nguyên mà nó sử dụng không được kernel thu hồi vì kernel nghĩ rằng tiến trình cha có thể sẽ cần dùng chúng. Điều này gây lãng phí tài nguyên hệ thống.  
EXIT_DEAD – Trạng thái chết  
Đây là trạng thái cuối cùng của một tiến trình. Tiến trình ở trạng thái này sẽ thực sự được kernel xóa khỏi hệ thống do tiến trình cha đã gọi wait4() system call.  
Trạng thái của một tiến trình được gán – thay đổi một cách rất đơn giản bằng việc thay đổi trường state của task_struct.  

**Truyền thông giữa các máy**  
Là trao đổi các dữ liệu giữa các máy với nhau.  
Các lệnh truyền thông:  
Terminal 1: Sender  
```$write<tên người nhận>[<tên trạm cuối>]```  
- <receiver> is not logged in  
- màn hình trắng để soạn thảo  
+  -o: Kết thúc 1 dòng  
+  -ô: Kết thúc dòng cuối cùng(hết thông báo).  
+  crt-d: Để kết thúc nối.  

Terminal 2: Receiver  
Message from user1  
Từ chối hoặc chấp nhận các message  
- $mesg<y|n>  
Mỗi người dùng đều được cấp 1 hộp thư riêng.  
$ mail: hỗ trợ việc gửi mail giữa các users  
- Message sau khi login: "you have mail"  
- Có 2 chế độ làm việc:  
+  command mode  
+  compose mode  

### Lập trình Bash Shell  
#### Khái niệm  
Shell script là một chương trình được sử dụng cho nhiều mục đích khác nhau, chẳng hạn như thực thi lệnh shell, chạy nhiều lệnh cùng nhau, tùy chỉnh các tác vụ quản trị, thực hiện tự động hóa,... mà bạn thường xuyên thực hiện trên máy tính của mình.  
Shell script cho phép chúng ta lập trình các lệnh theo một chuỗi và hệ thống sẽ thực thi chúng. Viết shell script cho phép bạn sử dụng các chức năng lập trình như các vòng lặp for, các câu lệnh if/then/else...  
Tiện ích của shell script:  
-  Nó có thể nhận đầu vào từ người dùng, tệp, hoặc kết quả từ màn hình.  
-  Giúp cho chúng ta có thể tạo nhóm lệnh riêng.  
-  Shell script giúp chúng ta tiết kiệm thời gian.  
-  Có khả năng thực hiện tự động một số công việc mà bạn thường xuyên trên máy tính của mình.  

Các tập lệnh được lưu trữ dưới dạng các tập tin có thể đặt tên tùy ý cho tập lệnh shell. Và nó bắt đầu với một shebang ngay dòng đầu tiên: #!/bin/bash  
Tiếp theo thì nó phải là một tập tin thực thi. Để có thể phân quyền cho tập tin là thực thi thì chúng ta sử dụng lệnh chmod: chmod u+x myscript  
Lệnh trên giúp cho tập tin myscript có thể thực thi được cho người dùng.  
Để comment cho 1 nội dung nào đó t sử dụng # <nội dung cần comment>  

#### Biến  
Biến là một chuỗi ký tự mà chúng ta có thể gán giá trị cho chúng. Giá trị được gán có thể là một số, văn bản, hoặc bất kỳ kiểu dữ liệu nào. Shell cho phép bạn tạo ra biến, gán giá trị, và xóa chúng.  

1. Đặt tên biến  
Tên biến bắt buộc phải đặt theo chuẩn mà Shell đưa ra.  
Tên biến chỉ chứa các ký tự từ a-z, các số từ 0-9 và ký tự gạch dưới _. Có thể dùng chữ in hoa hoặc in thường, tuy nhiên người ta quy ước nên đặt chữ in hoa vì nó là chuẩn chung.  

2. Gán giá trị cho biến  
Để gán giá trị cho biến thì bạn dùng cú pháp sau: variable_name=variable_value  

3. Truy xuất giá trị của biến  
Khi bạn muốn truy xuất đến một biến thì phải dùng ký tự đô la $ đặt trước biến đó.  

4. Biến chỉ đọc (giống hằng số)  
Biến chỉ đọc là biến chỉ cho phép đọc, không được phép thay đổi giá trị của biến.  
Để thiết lập một biến là chỉ đọc thì ta sử dụng từ khóa readonly.  

5. Xóa biến  
Nếu một biến không còn tác dụng gì cho chương trình thì nên xóa nó đi bằng cách sử dụng lệnh shell để xóa nó ra khỏi dành sách biến, sau khi xóa xong thì mất hoàn toàn biến đó.  
Để xóa biên thì ta dùng hàm unset, cú pháp như sau: unset variable_name  

**Có các loại biến như:**  
***Local Variables***  
Một biến nội bộ là một biến mà tồn tại trong trong quá trình thực thi của shell. Nó không có sẵn trong các chương trình mà được bắt đầu bởi Shell. Chúng được thiết lập tại dòng nhắc lệnh.  
***Environment Variables***  
 Biến môi trường là giá trị động ảnh hưởng đến phần mềm và tiến trình hoạt động trên server. Biến môi trường – environment variable có trên mọi hệ điều hành và có nhiều loại khác nhau. Biến môi trường có thể được tạo, chỉnh sửa, lưu hay xóa.  
***Shell Variables***  
Một biến shell là một biến đặc biệt mà được thiết lập bởi Shell và được yêu cầu bởi Shell để thực thi các hàm một cách chính xác. Một số biến này là biến môi trường, trong khi số khác là biến nội bộ.  
***Special Variables***  
Là biến được sinh ra bởi shell, giá trị của nó sẽ được cấp phát dựa vào dữ liệu đầu vào của chương trình shell, hoặc dữ liệu của chính hệ thống Linux.  

#### Toán tử và toán hạng  
Trong toán học, toán tử là các dấu hoặc ký hiệu như: cộng (+), trừ (-), nhân (x), chia (:), căn bậc 2 (√), lớn (>), bé (<), bằng (=),...  
Toán tử là công cụ dùng để thực hiện các phép tính hoặc chức năng với dữ liệu trong lập trình được thể hiện dưới dạng ký hiệu, biểu tượng nhằm thực hiện các biểu thức.  

Các toán tử cần biết:  
Toán tử số học  
-  +(phép cộng): Cộng 2 giá trị  
-  -(phép trừ): Trừ 2 giá trị  
-  *(phép nhân): Nhân 2 giá trị, phải thêm \* vì đây là ký tự đặc biệt  
-  /(phép chia): Chia 2 giá trị  
-  %(chia 2 giá trị): Chia lấy dư  
-  =(phép gán): Phép gán  
-  ==(phép so sánh): Phép so sánh bằng  
-  !=(phép so sánh không bằng): Phép so sánh không bằng  

Cú pháp:  
```expr toán_hạng_1 toán_tử toán_hạng_2```  

Toán tử quan hệ  
Toán tử quan hệ là toán tử so sánh giá trị giữa hai biểu thức, biểu thức có thể là một giá trị đơn hoặc một biểu thức dài với nhiều phép toán trong đó.  
-  -eq	So sánh bằng  
-  -ne	So sánh không bằng  
-  -gt	So sánh lớn hơn  
-  -lt	So sánh bé hơn  
-  -ge	So sánh lớn hơn hoặc bằng  
-  -le	So sánh bé hơn hoặc bằng  

Toán tử Boolean  
Boolean là kiểu dữ liệu có một trong hai giá trị là đúng hoặc sai, tức true hoặc false.  

Toán tử xử lí chuỗi  
-  =	So sánh hai chuỗi bằng nhau hay không  
-  !=	So sánh hai chuỗi khác nhau hay không  
-  -z	Kiểm tra chiều dài chuỗi có bằng 0 hay không (chuỗi rỗng)  
-  -n	Kiểm tra chiều dài chuỗi có lớn hơn 0 hay không  
-  str	Kiểm tra chuỗi str có khác rỗng hay không  

Toán tử kiểm tra file  
Dùng để kiểm tra file như kiểm tra định dạng, đường dẫn, kích thước file ...  
Khi sử dụng các toán tử này bạn phải chú ý đến quyền của file có hợp lệ hay không.  
-  -b file	Kiểm tra có phải là file khối đặc biệt  
-  -c file	Kiểm tra có phải file là file ký tự đặc biệt  
-  -d file	Kiểm tra file có phải là một thư mục  
-  -f file	Kiểm tra có phải là một file thông thường  
-  -g file	Kiểm tra file có được thiết lập group ID (SGID)  
-  -k file	Kiểm tra file có được thiết lập sticky bit  
-  -p file	Kiểm tra file có phải là file named pipe  
-  -t file	Kiểm tra trạng thái của file có đang mở bởi một terminal hay không  
-  -u file	Kiẻm tra file có được thiết lập User ID (SUID)  
-  -r file	Kiểm tra user có quyền đọc file hay không  
-  -w file	Kiểm tra user có quyền write trên file hay không  
-  -x file	Kiểm tra user có quyền execute file không  
-  -s file	Kiểm tra kích thước file có lớn hơn 0 hay không  
-  -e file	Kiểm tra file có tồn tại hay không  

#### Câu lệnh điều khiển  

**Câu lệnh rẽ nhánh If else**  
Lệnh If else đây là lệnh rẽ nhánh chương trình  
1. Lệnh if then fi  
Cú pháp  
```if [ expression ]  
then  
   # Thực hiện lệnh nếu expression true  
fi
```  
Shell sẽ kiểm tra điều kiện đầu vào expression có giá trị true hay false, nếu true thì thực thi chương trình bên trong lệnh then, sau đó kết thúc tại lệnh fi.  

2. Lệnh if else fi  
Nếu muốn expression trả về false sẽ thực hiện một chương trình khác thì có thể kết hợp thêm lệnh else.  
Cú pháp  
```if [ expression ]
then
   Chạy nếu expression true
else
   Chạy nếu expression false
fi
```  
Với chương trình này thì chương trình sẽ rẻ sang hai hướng và phụ thuộc vào biểu thức expression.  

3. Lệnh if elif fi  
Để có thể rẽ là 3 nhánh, 4 nhánh, ... bằng cách sử dụng kết hợp thêm lệnh elif.  
Cú pháp  
```if [ expression 1 ]
then
   Chạy nếu expression1 đúng
elif [ expression 2 ]
then
   Chạy nếu expression2 đúng
elif [ expression 3 ]
then
   Chạy nếu expression3 đúng
else
   Chạy nếu cả 3 biểu thức trên sai
fi
```
Có thể tạo nhiều hơn 3 nhánh và điều này phụ thuộc vào chương trình mà muốn viết.  

**Lệnh case...esac**  
Đây là câu lệnh rẽ nhánh có công dụng giống như if...else  
Cú pháp lệnh case .. esac trong shell script
Thực tế bạn có thể sử dụng lệnh if else để xử lý theo nhiều luồng khác nhau, tuy nhiên không phải lúc nào nó cũng tốt, nhất là trường hợp tất cả các luồng đều phụ thuộc vào một giá trị. Và trong trường hợp này bạn nên sử dụng lệnh case .. esac.  
Cú pháp:  
```case word in
   pattern1)
      Statement(s) 
      ;;
   pattern2)
      Statement(s) 
      ;;
   pattern3)
      Statement(s) 
      ;;
   *)
     Default 
     ;;
esac
```  
Trong đó:  
- word chính là giá trị mà bạn muốn dùng để rẻ nhánh chương trình thành nhiều luồng.  
- pattern1), pattern2), ... chính là các nhánh cho mỗi trường hợp.  
- Default sẽ được chạy nếu không có nhánh nào ở trên phù hợp.  

#### Vòng lặp  

***Vòng lặp while***  
Đây là vòng lặp cho phép lặp lại một nhóm lệnh cho đến khi điều kiện lặp trả về False.  
Vòng lặp while được sử dụng trong trường hợp ta chưa biết trước được tổng số lần lặp.  
Cú pháp vòng lặp while  
Vòng lặp while có cú pháp như sau:  
```while command
do
   Các lệnh sẽ chạy khi command trả về true
done
```
Điểm quan trọng nhất của vòng lặp while đó là kết quả trả về của command:  
-  Nếu command trả về true thì vòng lặp sẽ được chạy.  
-  Nếu command trả về false thì vòng lặp kết thúc.  

Có một số trường hợp các bạn chạy thuật toán bị sai dẫn đến command luôn trả về true, lúc này chương trình sẽ dẫn đến lặp vô hạn.  

***Vòng lặp for***  
Dùng để lặp một dãy số, một danh sách các thư mục / các file.  
Cú pháp:  
```for { tên biến } in { danh sách }
do
# Khối lệnh
# Thực hiện từng mục trong danh sách cho đến cho đến hết
# (Và lặp lại tất cả các lệnh nằm trong "do" và "done")
done

#hoặc sử dụng for
for (( expr1; expr2; expr3 ))
do
# Lặp cho đến khi biểu thức expr2 trả về giá trị TRUE
done
```  

***Vòng lặp until***  
Vòng lặp này tương tự với while  
Cú pháp:  
```until command
do
   Các lệnh sẽ chạy khi command true
done
```  
Trước khi lặp thì vòng lặp sẽ kiểm tra điều kiện command trả về true hay là false. Nếu trả về true thì lần lặp đó sẽ được lặp, ngược lại nếu trả về false thì vòng lặp sẽ kết thúc.  
Khi vòng lặp kết thúc thì trình biên dịch sẽ nhảy xuống phía dưới lệnh done, tức là chương trình vẫn tiếp tục chạy nếu phía dưới vòng lặp vẫn còn mã code.  

***Vòng lặp select***  
Vòng lặp select cung cấp một cách dễ dàng để tạo một menu được đánh số từ đó người sử dụng có thể chọn lựa. Nó là hữu ích khi bạn muốn hỏi người sử dụng để chọn một hoặc nhiều mục từ một danh sách các lựa chọn.  
Cú pháp:  
```select { tên biến } in { danh sách }
do
   cac lenh de thuc thi cho từng mục trong danh sách.
done
```  
#### Hàm  

**1. Khai báo hàm**  
Để khai báo hàm trong Bash shell, ta thực hiện như sau:  

```function fname()
{
    statements;
}
hoặc

fname()
{
    statements;
}
```  
với fname là tên của hàm.  

**2. Gọi hàm**  
Sau khi hoàn thành việc khai báo hàm, mỗi khi cần sử dụng đến hàm, ta gọi hàm:  
Đối với các hàm không có đối số $ fname  
Đối với các hàm có đối số, ta thêm danh sách các đối số phía sau tên hàm như sau: $ fname arg1 arg2 với arg1, arg2 là tên của các đối số.  

**3. Lấy giá trị đối số truyền vào hàm**  
Sau khi truyền các đối số vào hàm ở bước trên, để có thể sử dụng chúng bên trong hàm, chúng ta sử dụng các biến cục bộ:  
-  $1 => Đối số thứ 1  
-  $2 => Đối số thứ 2  
-  $n => Đối số thứ n  
-  “$@” => Danh sách tất cả các đối số được truyền vào.  
-  “$*” => In ra danh sách tất cả các đối số truyền vào dưới dạng 1 chuỗi  



