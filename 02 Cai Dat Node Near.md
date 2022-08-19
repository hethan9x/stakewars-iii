Các bạn chuẩn bị 01 VPS có cấu hình theo yêu cầu của bên Near:


| Hardware       | Chunk-Only Producer  Specifications                                   |
| -------------- | ---------------------------------------------------------------       |
| CPU            | 4-Core CPU with AVX support                                           |
| RAM            | 8GB DDR4                                                              |
| Storage        | 500GB SSD                                                             |

Mình có sẵn vps của Google Cloud. Nên trong bài viết này mình sẽ hướng dẫn các bạn cài đặt Node Near trên VPS của Google Cloud.

### Cài đặt NEAR-CLI

Kiểm tra VPS của bạn có phù hợp với yêu cầu của Near

```
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
  && echo "Supported" \
  || echo "Not supported"
```
> Supported

Nếu VPS của bạn hiểu thị "Supported" là ok.

