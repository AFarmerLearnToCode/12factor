## XII. Các process quản trị
### Chạy các tác vụ quản trị/quản lý dưới dạng process chạy một-lần (one-off process)

One-off processes: Các process (chỉ cần) chạy một lần - để tạo sự thay đổi đến hệ thống một lần và mãi mãi.

[Sự hình thành của process quản trị](./concurrency) là sự ra đời của hàng loạt các process được sử dụng để thực thi các nghiệp vụ thông thường của ứng dụng (như là điều khiển các requests tới web) khi chúng vận hành. Ngoài ra, lập trình viên thường muốn thực hiện các task quản trị chỉ một lần hoặc các task bảo trì cho ứng dụng như là: 

* Thực hiện chạy migrate (thay đổi cấu trúc, dữ liệu) cho database (dạng như lệnh `manage.py migrate` của Django, hay là `rake db:migrate` của Rails).
* Khởi tạo console (được biết đến như là [REPL](http://en.wikipedia.org/wiki/Read-eval-print_loop)) để chạy các đoạn code tuỳ ý hoặc kiểm tra các mô hình của ứng dụng đối với database hiện tại. Hầu hết các ngôn ngữ cung cấp REPL bằng cách chạy trình thông dịch không có tham số (như với `python` hoặc `perl`) hoặc trong vài trường hợp thì có các câu lệnh đặc biệt (như là `irb` với Ruby, `rails console` với Rails).
* Chạy các scripts một-lần mà được quản lý cùng trong source code của ứng dụng (như là `php scripts/fix_bad_records.php`).

Các process quản trị một-lần nên được chạy trong cùng một môi trường giống như [các process thông thường chạy lâu dài khác](./processes) của ứng dụng. Với một bản [phát hành](./build-release-run), các process quản trị sử dụng cùng [codebase](./codebase) và [cấu hình](./config) như bất kỳ các process vận hành trong bản phát hành đó. Code cho các tính năng quản trị cần được triển khai cùng với code của ứng dụng để đảm bảo không có các vấn đề về mặt động bộ hoá.

Các kỹ thuật [loại bỏ sự phụ thuộc](./dependencies) tương tự được sử dụng cho tất cả các kiểu process. Ví dụ một process của web sử dụng Ruby sử dụng câu lệnh `bundle exec thin start`, sau đó việc migrate database sử dụng câu lệnh `bundle exec rake db:migrate`. Tương tự, một chương trình Python sử dụng Virtualenv cần sử dung câu lệnh `bin/python` cho việc vận hành máy chủ web Tornado và bất cứ process quản trị thông qua `manage.py`.

"12 Yếu Tố" ưu tiên sử dụng các ngôn ngữ cung cấp REPL linh hoạt, và làm nó trở nên dễ dàng cho việc chạy các script một-lần. Trên môi trường local, lập trình viên thực thi các process quản trị bằng cách chạy trực tiếp các câu lệnh lưu trữ trong cùng thư mục chứa code của ứng dụng. Còn trên môi trường production, lập trình viên phải dùng tới ssh hoặc các cơ chế chạy câu lệnh từ xa khác nhau mà được cung cấp bởi môi trường vận hành của quá trình deploy để chạy các process.
