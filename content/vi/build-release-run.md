## V. Xây dựng, phát hành, vận hành
### Tách biệt hoàn toàn giữa bước xây dựng và vận hành

[Codebase](./codebase) được chuyển sang bước triển khai (không phải phát triển) thông qua ba bước:

* Giai đoạn build* là bước chuyển các đoạn mã thành các gói có khả năng thực thi được gọi là một *bản build*. Sử dụng phiên bản của mã nguồn ở một commit quy định bở quy trình triển khai, giai đoạn build lấy về và cung cấp các [phụ thuộc](./dependencies) và biên dịch các thành phần và tài nguyên.
* Giai đoạn release* sử dụng các kết quả của giai đoạn build và kết hợp với [cấu hình](./config) triển khai hiện tại. Kết quả của *phát hành* bao gồm cả bản build và các câu hình cho phép ứng dụng có thể được vận hành trong môi trường vận hành.
* Giai đoạn vận hành* (được biết như là "thời gian vận hành" (runtime)) vận hành ứng dụng trong môi trường thực thi, bằng việc thực thi một tập các [tiến trình](./process) của của ứng dụng với một phiên bản phát hành cụ thể.

![Mã nguồn được xây dựng, kết hợp với các cấu hình để cung cập một phát hành.](/images/release.png)

**Ứng dụng sử dụng "12 Yếu Tố" tách biệt hoàn toàn giữa các bước xây dựng, phát hành và vận hành.** Ví dụ, chúng ta không thể tạo ra các thay đổi của mã nguồn khi đang vận hành, do đó không có khả năng quay ngược lại bước xây dựng.

Công cụ triển khai thường cung cấp công cụ quản lý release, cùng với khả năng đặc biệt cho phép quay ngược lại bản phat hành trước đó. Ví dụ, công cụ triển khai [Capistrano](https://github.com/capistrano/capistrano/wiki) lưu trữ các phát hành trong thư mục con tên là `releases`, nơi mà phiên bản hiện tại được liên kết giả đến thư mục phát hành hiện tại. Lệnh `rollback` làm cho việc quay trở lại phiên bản trước trở nên dễ dàng. 

Mỗi phát hành đều có một định danh ID duy nhất, như là dựa vào thời gian phát hành (như `2011-04-06-20:32:17`) hoặc một số tự tăng (như `v100`). Các phiên bản được tạo ra thành một chuỗi liên tục và một phiên bản không thể thay đổi sau khi nó được tạo ra. Bất cứ thay đổi nào đểu tạo ra một bản phát hành mới.

Các bản build được khởi tạo bởi nhà phát triển ứng dụng mỗi khi mà mã nguồn được deploy. Đối với môi trường Runtime, ngược lại, có thể tự động chạy lại trong trường hợp các máy chủ được khởi động lại, hoặc tiến trình tạm dừng được khởi động lại bởi bộ quản lý các tiến trình. Do đó, bước vận hành nên được giữ các thành phần thay đổi càng ít càng tốt, vì các sự cố xảy ra làm ứng dụng không vận hành được có thể gây ra các thiệt hại lúc nửa đêm khi mà không có bất kỳ lập trình viên nào có thể khắc phục sự cố. Giai đoạn build có thể phức tạp hơn, vì các lỗi có thể xuất hiện lập tức cho lập trình viên, người đang thực hiện triển khai biết được.
