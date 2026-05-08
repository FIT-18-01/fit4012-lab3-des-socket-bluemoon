# Report 1 page - Lab 3

## Thông tin nhóm
- Thành viên 1: Nguyễn Như Thành
- Thành viên 2: Trần Việt trung

## Mục tiêu
Nguyễn Như Thành: Bài lab nhằm mục tiêu xây dựng hệ thống truyền tin bảo mật cơ bản giữa Sender và Receiver qua giao thức TCP Socket. Thông qua việc cài đặt thuật toán mã hóa DES ở chế độ CBC (Cipher Block Chaining) và cơ chế Padding PKCS#7, nhóm hiểu rõ quy trình đóng gói dữ liệu (Encapsulation), quản lý Vector khởi tạo (IV) và nhận diện các lỗ hổng bảo mật khi truyền khóa công khai trên đường truyền.

## Phân công thực hiện
Nguyễn Như Thành: Phụ trách phát triển chương trình sender.py, xây dựng mô hình phân tích rủi ro (Threat Model) và thiết kế kịch bản kiểm thử tấn công thay đổi dữ liệu (Tamper test).

Trần Việt Trung: Phụ trách phát triển chương trình receiver.py, viết báo cáo kỹ thuật và thiết kế kịch bản kiểm thử lỗi khóa (Wrong key test).

Phần làm chung: Xây dựng thư viện dùng chung des_socket_utils.py và thực hiện Peer Review mã nguồn.

## Cách làm
Sender: Đọc tin nhắn, sử dụng pycryptodome để mã hóa DES-CBC. Gói tin được đóng gói theo định dạng Header cố định: 8 byte Key, 8 byte IV, 4 byte độ dài bản mã, sau đó là nội dung bản mã.

Receiver: Lắng nghe kết nối, bóc tách Header theo đúng thứ tự để lấy Key/IV, sau đó tiến hành giải mã và gỡ bỏ Padding PKCS#7 để khôi phục văn bản gốc.

Kiểm thử: Sử dụng pytest để tự động hóa việc kiểm tra tính đúng đắn của Padding, Header và các trường hợp lỗi ngoại lệ (Negative tests).

## Kết quả
Hệ thống chạy thành công trên môi trường Local thông qua script demo_local.sh.

Ca kiểm thử quan trọng:

test_tamper_negative: Xác nhận hệ thống phát hiện/giải mã sai khi bản mã bị thay đổi.

test_wrong_key_negative: Xác nhận không thể khôi phục dữ liệu nếu dùng sai khóa.

Toàn bộ log chạy thực tế được lưu trữ tại thư mục logs/ minh chứng cho luồng dữ liệu khớp giữa Sender và Receiver.
## Kết luận
Bài học kỹ thuật: Hiểu sâu về cơ chế hoạt động của mã hóa khối (Block Cipher), tầm quan trọng của IV trong việc chống tấn công từ điển và cách quản lý luồng dữ liệu qua Socket.

Bài học bảo mật: Nhận thức được rằng việc gửi kèm Key/IV trong Header là một lỗ hổng nghiêm trọng. Trong thực tế, cần sử dụng các giao thức trao đổi khóa an toàn như Diffie-Hellman hoặc thiết lập kênh truyền TLS/SSL.
