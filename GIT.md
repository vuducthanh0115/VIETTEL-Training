# Tìm hiều về GIT
### 1. Những khái niệm chung
**Git là gì?**  
 Git là 1 phần mềm cài đặt trên máy tính giúp cho chúng ta có thể quản lí file, có thể biết được khi nào thì 1 file nào trong folder đó bị thay đổi bằng 1 lệnh git  
 Git cung cấp cho mỗi người kho lưu trữ (repository) riêng chứa toàn bộ lịch sử thay đổi.
 Git cung cấp cho mỗi lập trình viên kho lưu trữ (repository) riêng chứa toàn bộ lịch sử thay đổi.
 Lưu lại được các phiên bản khác nhau của mã nguồn dự án phần mềm  
 Khôi phục lại mã nguồn từ một phiên bản bất kỳ  
 Dễ dàng so sánh giữa các phiên bản  
 Phát hiện được ai đã sửa phần nào làm phát sinh lỗiKhôi phục lại tập tin bị mất  
 Dễ dàng thử nghiệm, mở rộng tính năng của dự án mà không làm ảnh hưởng đến phiên bản chính  
 Giúp phối hợp thực hiện dự án trong nhóm một cách hiệu quả  
**Git repository là gì?**  
 Repository hay còn được gọi là repo.     
 Git repository là 1 nơi chứa tất cả các mã nguồn cho 1 dự án được quản lí bởi Git. 
 Trong Repo có 2 cấu trúc dữ liệu chính là Object Store và Index. Tất cả dữ liệu của Repo đều được chứa trong thư mục bạn đang làm việc dưới dạng folder ẩn có tên là .git.  
 Repository của Git được phân thành 2 loại : remote repository và local repository.  
- Remote repository: Là repository để chia sẻ giữa nhiều người và bố trí trên server chuyên dụng.  
- Local repository: Là repository bố trí trên máy của bản thân mình, dành cho một người dùng sử dụng.  

**Git & Github & Gitlab giống/khác gì nhau?**   
Git là một hệ thống kiểm soát phiên bản phân tán mã nguồn mở có sẵn cho tất cả mọi người với chi phí bằng không. Nó được thiết kế để xử lý các dự án từ nhỏ đến lớn với tốc độ và hiệu quả. Nó được phát triển để điều phối công việc giữa các lập trình viên. Kiểm soát phiên bản cho phép bạn theo dõi và làm việc cùng với thành viên trong nhóm của mình tại cùng một không gian làm việc.  
GitHub cũng là một nền tảng lưu trữ online lớn về các dự án nhiều người làm.  
GitLab là hệ thống self-hosted mã nguồn mở dựa trên hệ thống máy chủ Git dùng để quản lý mã nguồn của bạn. GitLab cung cấp giải pháp server một cách hoàn hảo  
**Phân biệt :**  
- Git là một công cụ kiểm soát phiên bản phân tán có thể quản lý lịch sử mã nguồn còn GitHub và GitLab là một công cụ dựa trên đám mây được phát triển xung quanh công cụ Git.  
- Git là 1 công cụ cục bộ còn GitHub và GitLab là một dịch vụ trực tuyến để lưu trữ code và đẩy từ máy tính chạy công cụ Git.  
- Git tập trung vào kiểm soát phiên bản và chia sẻ code còn GitHub và GitLab tập trung vào lưu trữ code  
- Git là 1 công cụ dòng lệnh còn GitHub và GitLab được quản lí thông qua trang web.  
- Git không cung cấp bất kỳ tính năng quản lý người dùng nào còn GitHub và GitLab được tích hợp sẵn tính năng quản lý người dùng.  
 
**Các trạng thái có thể có trong git repository**   
Repo của Git được phân thành 2 loại : remote repo và local repo.  
Các trạng thái có thể có của file trong repo : 
<img src="https://github.com/vuducthanh0115/img/blob/main/anh/1.png" width="800" height="400" />  

**Untracked Files**: Nếu tạo ra hoặc thêm vào một tập tin mới vào trong thư mục làm việc của mình thì nó sẽ ở trạng thái Untracked.        
**Tracked Files**: Những files đã được thêm vào danh sách theo dõi của git được gọi là Tracked Files, những file này khi chúng ta thay đổi / thêm / xoá thì git sẽ nhận biết được điều đó và lưu các thay đổi này lại theo yêu cầu của chúng ta.  
**Modified Files**: Ta thay đổi tập tin nhưng chưa commit vào cơ sở dữ liệu có nghĩa chưa sử dụng lệnh git add và git commit.    
**Staged Files**: Staged là đã đánh dấu sẽ commit phiên bản hiện tại của một tập tin đã chỉnh sửa trong lần commit sắp tới. VD sử dụng lệnh git add <file_name> nhưng chưa commit.    
**Unmodified Files**: File được Git quản lí nhưng không có thay đổi gì.  

**2. Config cho git với git config**  
- Config thông tin cá nhân  
- Config default/prefered editor  
- Config global .gitignore  
*Các lệnh cấu hình :*  
$ git config --global user.name "<name>"  
$ git config --global user.email <mail>  
$ git config --global core.editor "'C:\Program Files\Notepad++\notepad++.exe' -multiIns -nosession"  
 <img src="https://github.com/vuducthanh0115/img/blob/main/anh/2.png" width="800" height="400" />  
 
**3. Các thao tác ban đầu**  
**Khởi tạo repo với git init**
Lệnh git init được sử dưng để tạo, khởi tạo một kho chứa Git mới (Git Repo) ở local. Khi đang trong thư mục dự án chạy lệnh git init nó sẽ tạo ra một thư mục con (ẩn) tên .git, thư mục này chứa tất cả thông tin mô tả cho kho chứa dự án (Repo) mới - những thông tin này gọi là metadata gồm các thư mục như objects, refs ... Có một file tên HEAD cũng được tạo ra - nó trỏ đến commit hiện tại.  
Lệnh: $ git init  

 <img src="https://github.com/vuducthanh0115/img/blob/main/anh/3.png" width="800" height="400" />  
 
**4. Git commit**  
**Commit trong git là gì ?**  
Commit là thao tác báo cho hệ thống biết mình muốn lưu lại trạng thái hiện hành, ghi nhận lại lịch sử các xử lý như đã thêm, xóa, cập nhật các file hay thư mục nào đó trên repo.  
Khi thực hiện commit, trong repo sẽ ghi lại sự khác biệt từ lần commit trước với trạng thái hiện tại. Các commit ghi nối tiếp với nhau theo thứ tự thời gian.  
**Một commit chứa những thông tin gì ?**  
Một commit chứa tất cả những thay đổi của mình tất cả những gì mình đã làm và có ngày giờ cụ thể tại thời điểm chúng ta thay đổi.
**Amending - Thay Đổi Commit Cuối Cùng**  
- Khi chúng ta commit nhưng bị quên add một số file nào đó và không muốn tạo ra một commit mới thì có thể sử dụng lệnh $ git commit --amend để gộp các file đó và bổ sung vào commit cuối cùng, vì vậy không tạo ra commit mới.  
- Muốn loại bỏ một file ra khỏi stage thì sử dụng lệnh $ git reset HEAD <file_name>.  

**5. Làm việc với branch**
Branch là những phân nhánh ghi lại luồng thay đổi của lịch sử, các hoạt động trên mỗi branch sẽ không ảnh hưởng lên các branch khác nên có thể tiến hành nhiều thay đổi đồng thời trên một repo, giúp giải quyết được nhiều nhiệm vụ cùng lúc.    
Khi tham gia dự án với mỗi nhiệm vụ chúng ta sẽ tạo một branch và làm việc trên đó, các branch này sẽ hoạt động riêng lẻ và không ảnh hưởng lẫn nhau.  
 
**Tạo mới branch**  
 Để tạo 1 branch mới ta sử dụng lệnh : $ git branch <branchname>
 
 <img src="https://github.com/vuducthanh0115/img/blob/main/anh/4.png" width="800" height="400" />
 
**==>**	Khi tạo mới nhánh thì nhánh master và test đều trỏ tới cái commit hiện tại.  
 
**Nhảy từ branch này sang branch khác**  
Khi nhảy từ branch này sang branch khác ta dùng câu lệnh: >$ git checkout <branch_name>
 <img src="https://github.com/vuducthanh0115/img/blob/main/anh/5.png" width="800" height="400" />
 
**Đổi tên branch**  
Muốn đổi tên branch ta dùng lệnh: $ git branch -m <oldbranch> <newbranch>  
 <img src="https://github.com/vuducthanh0115/img/blob/main/anh/6.png" width="800" height="400" />  
 
**6. Git checkout**  
Lệnh git checkout được dùng để chuyển nhánh hoặc để phục hồi file trong thư mục làm việc từ một commit trước đây .  
VD ta đang ở nhánh nào đó muốn chuyển sang nhánh master thì thực hiện lệnh: $ git checkout master  
Lúc này nhánh master hoạt động, và thư mục làm việc là các file tương ứng với nhánh này  
 <img src="https://github.com/vuducthanh0115/img/blob/main/anh/7.png" center width="800" height="400" />  

**7. Các thao tác liên quan khác**  
**Git Merge**  
Git Merge là một lệnh dùng để hợp nhất các chi nhánh độc lập thành một nhánh duy nhất trong Git.  
Khi sử dụng lệnh hợp nhất trong Git, chỉ có nhánh hiện tại được cập nhật để phản ánh sự hợp nhất, còn nhánh đích sẽ không bị ảnh hưởng.  
Để merge một branch bất kì vào branch hiện tại thì bạn sử dụng lệnh: 
$ git merge <branch_name>  

**Git Rebase**  
Git Rebase là một chức năng được dùng khi gắn nhánh đã hoàn thành công việc vào nhánh gốc . Việc điều chỉnh nhánh công việc gắn vào với nhánh gốc nên các commit sẽ được đăng kí theo thứ tự gắn vào .  
Câu lệnh : $ git rebase <namebranch>  
 <img src="https://github.com/vuducthanh0115/img/blob/main/anh/8.png" width="800" height="400" />  
 
**Git Pull**  
Git Pull là một lệnh dùng để tải xuống dữ liệu từ một Remote repo và cập nhật Local repo phù hợp với dữ liệu đó. Có nghĩa là Git Pull là lệnh hợp nhất các thay đổi từ Remote repo vào Local repo.  
**Git Push**  
Lệnh git push được sử dụng để đẩy các commit mới ở local repo lên remote repo. Nguồn để đẩy lên là nhánh mà con trỏ HEAD đang trỏ tới (nhánh làm việc).  
Lệnh git push cũng có thể xóa đi các nhánh của remote.  
Một số tham số hay dùng như:  
- all đẩy tất cả các nhánh lên server
- tags đẩy tất cả các tag lên server
- delete xóa một nhánh chỉ ra trên server 
- u đẩy và tạo một upstream (luồng upload tương ứng với nhánh của local), hay sử dụng cho lần đầu đẩy lên server  

*Đẩy lên server lần đầu tiên*  
 Nếu là lần đầu tiên đẩy Local Repo lên Remote Repo mới khởi tạo thì cần tạo ra một theo dõi kết nối, upstream giữa local và remote, vậy hãy dùng tham số -u. Ví dụ đẩy lên remote có tên origin và tạo upstream cho nhánh master  
 Lệnh : $ git push -u origin master  
*Đẩy lên server*  
 Sau khi có upstream, mỗi lần cần đẩy dữ liệu lên remote của nhánh master, chỉ việc thực hiện lệnh  
 Lệnh : $ git push  
*Đẩy lên server tất cả các nhánh*  
 Đẩy tất cả các nhánh ở local lên server có tên origin:  
 Lệnh : $ git push origin --all  
*Xóa một nhánh trên remote*  
 VD xóa nhánh test, trên remote có tên origin  
 Lệnh : $ git push origin --delete test  
*Ghi đè nhánh với --force*  
 Có thể ghi đè toàn bộ một nhánh ở remote bởi một nhánh ở master  
 VD ghi đè toàn nhánh master ở remote, giống với master của local  
 Lệnh : $ git push --force origin master  
 
**Git Rebase interactive**  
Khi chúng ta commit thiếu file lên git server hoặc ghi nội dung comment chưa được như ý muốn hoặc nội dung comment chưa đúng theo quy tắc chung đã đưa ra. Thì để sửa nội dung đã commit chúng ra có thể sử dụng lệnh : $ git rebase -i  
  <img src="https://github.com/vuducthanh0115/img/blob/main/anh/9.png" width="800" height="400" />  
 
**Git Cherry-pick**  
 Là một cách để checkout 1 commit bất kỳ tại 1 branch được chỉ định về brach hiện tại. Hay chính là git cherry-pick sẽ lấy thay đổi của 1 commit trên 1 nhánh nào đó áp dụng vào nhánh hiện tại.  
 
**Tùy chọn force**  
 Lệnh : git push -f origin master cho phép push kho lưu trữ cục bộ đến từ xa mà không cần giải quyết xung đột. Cách này khá nguy hiểm vì theo cơ chế, nó sẽ ghi đè lên remote repo bằng code ở local của mình, mà không cần quan tâm đến việc bên phía remote đang chứa thứ gì.
Cách push an toàn : sử dụng push --force-with-lease, git sẽ từ chối việc update lên branch trừ khi branch đó nằm trong trạng thái "được coi là an toàn". 
**Git reset**  
Git reset được dùng để quay về một điểm commit nào đó, đồng thời xóa lịch sử của các commit trước nó.  
Sử dụng reset để xóa commit : $ git reset --hard HEAD  
Sử dụng reset để xóa commit : $ git reset --hard HEAD  

**8. Các thao tác với git remote**  
**Add remote**  
Để thêm một remote repo vào local repo thì bạn sử lệnh: $ git remote add [shortname] [url]  
Trong đó:  
- shortname: là tên mà bạn muốn đặt cho remote repo  
- url: là đường dẫn trỏ đến repo, phần đuôi của URL sẽ là .git  
 
**Rename remote**  
Để đổi tên cho remote thì bạn sử dụng lệnh sau : $ git remote rename old_name new_name  
 
**Update remote**  
Để cập nhật dữ liệu từ remote repo về local repo thì ta sử dụng lệnh git fetch hoặc lệnh git pull.   
Lệnh git fetch tải về dữ liệu từ Remote Repo (các dữ liệu như các commit, các file, refs), dữ liệu tải về để chúng ta theo dõi sự thay đổi của remote, tuy nhiên tải về bằng git fetch nó chưa tích hợp thay đổi ngay local repository, mục đích để theo dõi các commit người khác đã cập nhật lên server, để có được thông thông tin khác nhau giữa remote và local.  
Lệnh git pull lấy về thông tin từ remote và cập nhật vào các nhánh của local repo.  

**Prune remote branch**  
Lệnh : $ git remote prune.  
Xóa các ref cho các nhánh không tồn tại trên remote.   
Nó loại bỏ các nhánh từ xa không có đối tác cục bộ. Ví dụ : nếu có một nhánh từ xa nói bản demo, nếu nhánh này không tồn tại cục bộ, thì nó sẽ bị xóa.  
 
**9. Các thao tác với Stash**  
**Tổng quan về git stash**  
Lệnh git stash sẽ có tác dụng với tất cả dữ liệu đang hoạt động trong working directory với điều kiện là dữ liệu đó đã được đưa vào trạng thái Staged hoặc đã từng được committed.  
**git stash list**  
Xem danh sách bao nhiêu lệnh stash đã dùng.   
Nếu chúng ta đã stash rất nhiều lần và muốn xem danh sách và địa chỉ của nó thì sử dụng lệnh :
$ git stash list  
**git stash clear**  
Nếu chúng ta muốn xóa tất cả stash ra khỏi history thì sử dụng tham số clear
Lệnh : $ git stash clear  
 
**==>**	Lúc này danh sách stash sẽ rỗng.  
