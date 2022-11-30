## I. Codebase
### Codebase được theo dõi với hệ thống quản lý phiên bản, và nhiều lần triển khai (deploy)

Một ứng dụng "12 Yếu Tố" luôn luôn được theo dõi bới hê thống quản lý phiên bản, như là [Git](http://git-scm.com/), [Mercurial](http://mercurial.selenic.com/), hay [Subversion](http://subversion.apache.org/). Một bản lưu của cơ sở dữ liệu các phiên bản được gọi là **code repository**, và hay được viết vắn tắt thành *code repo* hay *repo*.

Một *codebase* là bất kì một repo riêng lẻ (trong một hệ thống quản lý phiên bản thống nhất như Subversion), hoặc bất kì một nhóm các repo chia sẻ cùng một commit nguồn (root commit) (trong một hệ thống quản lý phiên bản kiểu phân quyển như Git).

![Chỉ có một codebase tương ứng với nhiều bản triển khai](/images/codebase-deploys.png)

Sẽ luôn luôn là sự tương quan một-với-một giữa codebase và ứng dụng:

* Nếu có nhiều codebase, đấy không phải là một ứng dụng -- mà là một hệ thống phân tán. Với các
phần tử trong một hệ thống phân tán là một ứng dụng, với mỗi cá thể tuân theo luật "12 Yếu Tố".
* Nhiều ứng dụng chia sẻ cùng một bộ mã nguồn là vi phạm luật của "12 Yếu Tố". Giải pháp để giải quyết là xem xét
để nhóm các mã chia sẻ thành các thư viện mà có thể được nhúng vào thông qua [trình quản lý các gói phụ thuộc (dependency manager)](./dependencies).

Chỉ có một codebase từng ứng dụng, nhưng sẽ có nhiều triển khai của một ứng dụng. Một *triển khai* là một đối tượng thực thi của ứng dụng đó. Đây là trường hợp rất phổ biến của các trang
đã đi vào hoạt động, và của một vài trang thử nghiệm. Thêm vào đó mỗi lập trình viên sẽ có một
bản lưu của ứng dụng đang chạy trên môi trường phát triển cá nhân, mỗi bản đều được coi như là
một bản triển khai.

Codebase sẽ giống nhau trên các bản triển khai, tuy là phiên bản khác nhau có thể hoạt dộng trong mỗi bản triển khai. Lấy một ví dụ, một lập trình viên có nhiều commit nhưng chưa deploy vào
môi trường thử nghiệm (staging); môi trường thử nghiệm có nhiều commit mà chưa được triển khai trên môi trường production. Nhưng cả hai đều chia sẻ cùng một codebase; vì vậy phải định dạng chúng
như những bản triển khai của cùng một ứng dụng.
