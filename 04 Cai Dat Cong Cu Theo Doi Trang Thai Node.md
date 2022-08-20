### Theo dõi trạng thái của node qua lệnh trên vps

Xem lịch sử chạy của node một cách trực quan (có màu sắc) bạn cài đặt thêm công cụ CCZE

```
sudo apt install ccze
```

Xem lịch sử chạy của node

```
journalctl -n 100 -f -u neard | ccze -A
```

![img](./image/Theo-doi-node-01.png)

### Theo dõi trạng thái của node trên website

Cài đặt

```
sudo apt install curl jq
```

Kiểm tra

```
curl -s http://127.0.0.1:3030/status | jq .version
```

Để theo dõi trạng thái của nên trên website chúng ta cần mở port 3030. Google Cloud có hệ thống firewall được quản lý trên console nên việc sử dụng firewall trên vps là không cần thiết. Vì vậy đầu tiên các bạn tắt firewall mặc định của vps sau đó sẽ mở port trên firewall của Google Cloud.

#### Tắt firewall trên vps

```
sudo ufw disable
```

![img](./image/Theo-doi-node-02.png)

#### Mở port 3030 trên firewall của Google Cloud

Trên trang console của Google Cloud bạn kích vào dấu 3 gạch -> chọn VPC network -> chọn Firewall

![img](./image/Theo-doi-node-03.png)

Kích vào " Create Firewall Rule"

![img](./image/Theo-doi-node-04.png)

Bạn điền thông tin như hình ảnh bên dưới. Sau đó kích chọn "Create"

* Name: tên của rule
* Targets: All instances in the network
* IPv4 ranges: Source filte
* Source IPv4 range: 0.0.0.0/0
* Protocols and ports: Specified protocols and ports TCP: 3030 /  UDP: 3030

![img](./image/Theo-doi-node-05.png)

![img](./image/Theo-doi-node-06.png)

Như vậy đã mở port 3030 thành công trên vps của bạn. Bạn có thể xem trạng thái của node theo đường dẫn:

http://ip_public:3030/status

http://ip_publuc:3030/debug

### Theo dõi trạng thái của node bằng bot thông báo trên Telegram

Mình sẽ hướng dẫn các bạn sử dụng script của Klesh, setup bot Telegram sẽ báo mỗi khi node của bạn có sự thay đổi như khi node ONLINE / KICKED OUT / Đang Validator … tất cả sẽ thông báo về Telegram của bạn.
"Nguồn: https://github.com/Klesh-/near-protocol-node-telegram-notifications"

Bạn cần có tài khoản teleram, việc tạo tài khoản mình không hướng dẫn vì khi tham gia vào crypto chắc chắn ai cũng có telegram rồi.

Tiếp theo bạn tạo 1 con bot cho mình trên telegram tại https://t.me/BotFather 

Kích vào Start sau đó chọn /newbot nhập tên bot mà bạn muốn tạo enter. 

Khi tạo xong bot màn hình sẽ hiển thị HTTP API và url bot của bạn mới tạo. Bạn lưu lại HTTP API

![img](./image/Theo-doi-node-07.png)

Kích vào url bot của bạn và nhấn Start để cho phép bot gửi tin nhắn cho bạn

Truy cập bot  https://t.me/cid_bot, kích Start. Bạn sẽ hiện thị Your ChatID, Bạn lưu lại Chat ID.

![img](./image/Theo-doi-node-08.png)

SSH vào VPS và thực hiện các lệnh sau

```
cd

git clone https://github.com/Klesh-/near-protocol-node-telegram-notifications.git

cd near-protocol-node-telegram-notifications

cp .env.example .env

sudo chmod +x ./report_node_status.sh


```
![img](./image/Theo-doi-node-09.png)

Sửa file .env

```
nano .env
```

* TG_API_KEY là HTTP API
* TG_CHAT_ID là ChatId
* POOL_ID sửa thành id của ví của bạn

![img](./image/Theo-doi-node-10.png)

Nhấn Ctrl + O và enter để lưu file lại. Bấm Ctrl + X để thoát ra.

Đã cấu hình xong, chạy thử bằng lệnh

```
./report_node_status.sh
```

Như vậy mình đã giới thiệu đầy đủ cho bạn 3 cách để theo dõi trạng thái của Node. Hiện tại mình đang dùng cả 3 cách này. Các bạn chọn cho mình một cách phù hợp nhé!

### Sau khi hoàn thành việc khởi tạo một trình xác nhận bạn sẽ nhận được số điểm là 15 UNP (tương đương với 15 near được mở khoá)

