## Chuẩn bị VPS (VPS Google Cloud)
Các bạn chuẩn bị 01 VPS có cấu hình theo yêu cầu của bên Near:


| Hardware       | Chunk-Only Producer  Specifications                                   |
| -------------- | ---------------------------------------------------------------       |
| CPU            | 4-Core CPU with AVX support                                           |
| RAM            | 8GB DDR4                                                              |
| Storage        | 500GB SSD                                                             |

Cài đặt hệ điều hành ubuntu 20.04 LTS.

Google Cloud đang có chương trình dùng thử cho khách hàng mới, bạn sẽ nhận được khoản tín dụng 300 USD để sử dụng trong 3 tháng. Nên trong bài viết này mình hướng dẫn các bạn cài đặt Node Near trên Google Cloud. Như vậy đã SSH được tới VPS của Google Cloud.

## Cài đặt NEAR-CLI

Để SSH vào VPS của Google Cloud các bạn vào Console của Google Cloud, kích vào mũi tên xuống bên cạnh chữ "SSH" chọn "Open in browser window" sẽ có một cửa sổ trình duyệt mở ra. 

### Kiểm tra VPS của bạn có phù hợp với yêu cầu của Near

```
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
  && echo "Supported" \
  || echo "Not supported"
```
> Supported

Nếu VPS của bạn hiểu thị "Supported" là ok.

![img](./image/Near-CLI-01.png)

### Cập nhật VPS

```
sudo apt update && sudo apt upgrade -y
```
### Cài đặt Node.js and npm

```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
sudo apt install build-essential nodejs
PATH="$PATH"
```
Khi được hỏi "Do you want to continue? [Y/n]", bạn chọn Y và Enter để tiếp tục

![img](./image/Near-CLI-02.png)

### Kiểm tra phiên bản Node.js và npm
```
node -v
```

```
npm -v
```
![img](./image/Near-CLI-03.png)

### Cài đặt NEAR-CLI

```
sudo npm install -g near-cli
```
![img](./image/Near-CLI-04.png)
