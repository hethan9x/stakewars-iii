### Chuẩn bị VPS (VPS Google Cloud)
Các bạn chuẩn bị 01 VPS có cấu hình theo yêu cầu của bên Near:


| Hardware       | Chunk-Only Producer  Specifications                                   |
| -------------- | ---------------------------------------------------------------       |
| CPU            | 4-Core CPU with AVX support                                           |
| RAM            | 8GB DDR4                                                              |
| Storage        | 500GB SSD                                                             |

Cài đặt hệ điều hành ubuntu 20.04 LTS.

Google Cloud đang có chương trình dùng thử cho khách hàng mới, bạn sẽ nhận được khoản tín dụng 300 USD để sử dụng trong 3 tháng. Nên trong bài viết này mình hướng dẫn các bạn cài đặt Node Near trên Google Cloud.

### Cài đặt NEAR-CLI

Kiểm tra VPS của bạn có phù hợp với yêu cầu của Near

```
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
  && echo "Supported" \
  || echo "Not supported"
```
> Supported

Nếu VPS của bạn hiểu thị "Supported" là ok.

