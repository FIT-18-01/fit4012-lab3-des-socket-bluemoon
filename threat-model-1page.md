# Threat Model - Lab 3

## Thông tin nhóm
- Thành viên 1: Nguyễn Như Thành
- Thành viên 2: Trần Việt Trung

## Assets
Nguyễn Như Thành: Tin nhắn gốc, Khóa DES (8 byte), Vector khởi tạo IV (8 byte).

## Attacker model
Nguyễn Như Thành: Kẻ tấn công đứng giữa (Man-in-the-Middle) trên mạng LAN, có khả năng bắt gói tin TCP (Sniffing).

## Threats
Nguyễn Như Thành:
Lộ dữ liệu nhạy cảm: Kẻ tấn công lấy được Key/IV trực tiếp từ Header để giải mã bản tin.

Tấn công toàn vẹn: Thay đổi nội dung bản mã làm sai lệch thông tin nhận được.

Tấn công phát lại: Thu thập gói tin và gửi lại cho Receiver nhiều lần.

## Mitigations
Nguyễn Như Thành:

Sử dụng giao thức TLS để bảo vệ toàn bộ luồng dữ liệu.

Triển khai trao đổi khóa Diffie-Hellman thay vì gửi trực tiếp qua Header.

Sử dụng HMAC để đảm bảo tính toàn vẹn và xác thực nguồn gốc.

## Residual risks
Nguyễn Như Thành:
Rủi ro từ việc quản lý chìa khóa tại máy trạm và lỗ hổng cố hữu của thuật toán DES (độ dài khóa ngắn).
