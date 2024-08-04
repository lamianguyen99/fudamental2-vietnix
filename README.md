# Kiến thức cơ bản LINUX LP1 - Vietnix

[Kiểm tra và giám sát hệ thống](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#ki%E1%BB%83m-tra-v%C3%A0-gi%C3%A1m-s%C3%A1t-h%E1%BB%87-th%E1%BB%91ng)

[Quản lý FILE và thư mục](https://github.com/lamianguyen99/fudamental2-vietnix/tree/main?tab=readme-ov-file#qu%E1%BA%A3n-l%C3%BD-file-v%C3%A0-th%C6%B0-m%E1%BB%A5c)

[Truyền FILE và sao lưu dữ liệu](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#truy%E1%BB%81n-file-v%C3%A0-sao-l%C6%B0u-d%E1%BB%AF-li%E1%BB%87u)

[Xử lý và chỉnh sửa văn bản](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#x%E1%BB%AD-l%C3%BD-v%C3%A0-ch%E1%BB%89nh-s%E1%BB%ADa-v%C4%83n-b%E1%BA%A3n)

[Chẩn đoán và xác định vấn đề mạng](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#ch%E1%BA%A9n-%C4%91o%C3%A1n-v%C3%A0-x%C3%A1c-%C4%91%E1%BB%8Bnh-v%E1%BA%A5n-%C4%91%E1%BB%81-m%E1%BA%A1ng)

---

## Kiểm tra và giám sát hệ thống

    
### Ping/hping3: Kiểm tra kết nối mạng.

Lệnh `ping vietnix.vn` 
    
**Kết quả:**

```
ping vietnix.vn
PING vietnix.vn (14.225.253.240) 56(84) bytes of data.

64 bytes from static.vnpt.vn (14.225.253.240): icmp_seq=2 ttl=53 time=3.78 ms
64 bytes from static.vnpt.vn (14.225.253.240): icmp_seq=3 ttl=53 time=4.66 ms
64 bytes from static.vnpt.vn (14.225.253.240): icmp_seq=4 ttl=53 time=3.73 ms
```

**Giải thích:**
    
`seq=2`: Số thứ tự của gói tin ICMP trong trường hợp này đây là gói tin thứ 2 trong chuỗi.

`ttl=53`: TTL(Time to live) là một giá trị được sử dụng để kiểm soát số lần một gói tin ***ICMP echo request*** có thể được chuyển tiếp (Forward) trước khi bị loại bỏ. Giá trị 53 Cho thấy gói tin đã đi qua 53 router trước khi đến được đích.

`time=3.78 ms`: Đây là thời gian phản hồi, tức là thời gian gói tin ***ICMP echo reply*** đi từ máy tính nhận trở về. Trong TH này thời gian phản hồi là 3.78 ms.

> Tương tự với lệnh `hping3 --icmp vietnix.vn`

### Netstat: Hiển thị thông tin về các kết nối mạng.



ps: Hiển thị thông tin về các tiến trình đang chạy.
    
top: Hiển thị thông tin về các tiến trình đang chạy và mức độ sử dụng tài nguyên.
    
free: Hiển thị thông tin về bộ nhớ.

df: Hiển thị thông tin về dung lượng ổ đĩa.


## Quản lý FILE và thư mục

    cat: Hiển thị nội dung của tệp.
    
    echo: In ra văn bản.
    
    tail/head: Hiển thị một phần nội dung của tệp.
   
    find: Tìm kiếm tệp và thư mục.
   
    cp: Sao chép tệp.
   
    mv: Di chuyển hoặc đổi tên tệp.
   
    rm: Xóa tệp.
    
    ls: Liệt kê các tệp và thư mục.
   
    chmod, chown, chattr: Thay đổi quyền và thuộc tính của tệp và thư mục.
    
    ln: Tạo liên kết (symbolic link và hard link).



## Truyền FILE và sao lưu dữ liệu


### SSH: Kết nối và thực hiện lệnh trên máy chủ từ xa.

**Lưu ý: Trước khi dùng ssh cần đảm bảo clien-server đều đã mở port 22(ssh)**

***1. Lệnh SSH dùng Password:***
    Cú pháp: `ssh username@remote_host`
   
    Ví dụ:  `ssh huynet@192.168.0.9`

   Sau khi chạy lệnh này, bạn sẽ được nhắc nhập **password** của tài khoản username trên máy chủ từ xa remote_host.
   
   **Kết quả:**
   
   ```
   huydang@haionet:~$ sudo ssh huynet@192.168.1.9
   huynet@192.168.1.9's password: 

   Last login: Sun Aug  4 19:48:20 2024 from 192.168.1.5
   huynet@haionet:~$ 
   ```
   
***2. Lệnh SSH dùng key:***

Để thực hiện việc này, bạn cần thực hiện các bước sau:

- Tạo cặp SSH key (public key và private key) trên máy tính của bạn:

    `ssh-keygen -t rsa -b 4096`

**Thực hiện:**

![keygenSSH](https://github.com/user-attachments/assets/d1b3d535-0227-433e-9359-6d04d00d3ec9)


   Lệnh này sẽ tạo ra một cặp key RSA 4096-bit, được lưu trữ mặc định trong thư mục ~/.ssh/ với tên là id_rsa (private key) và id_rsa.pub (public key).

- Sao chép public key lên máy chủ từ xa:

    `ssh-copy-id username@remote_host`

    or

    `ssh-copy-id -i ~/PATH/id_rsa.pub username@remote_host`

**Thực hiện:**

```
huydang@huynet-vnx:~/ssh$ sudo ssh-copy-id -i /home/huydang/ssh/id_rsa.pub huynet@192.168.1.9                                                                   /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/huydang/ssh/id_rsa.pub"                                                                    /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed                                              /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys                                            
huynet@192.168.1.9's password:                                                         Number of key(s) added: 1          Now try logging into the machine, with:   `ssh huynet@192.168.1.9` and check to make sure that only the key(s) you wanted were added. ```                                          

    Lệnh này sẽ sao chép public key của bạn (id_rsa.pub) lên tài khoản username trên máy chủ từ xa remote_host. Sau khi thực hiện xong, public key của bạn sẽ được lưu trữ trong file ~/.ssh/authorized_keys trên máy chủ từ xa.

- Kết nối đến máy chủ từ xa bằng SSH, sử dụng private key:

    `ssh -i ~/.ssh/id_rsa username@remote_host`

**Kết quả:**
   
```
huydang@haionet:~/ssh$ sudo ssh -i /home/huydang/ssh/id_rsa huynet@192.168.1.9 

Last login: Sun Aug  4 21:32:03 2024 from 192.168.1.5
huynet@haionet:~$ 
```


Ở đây, tùy chọn -i cho phép bạn chỉ định đường dẫn đến private key (id_rsa) trên máy tính của bạn. SSH sẽ sử dụng private key này để xác thực với máy chủ từ xa, thay vì yêu cầu bạn nhập mật khẩu.

Lưu ý rằng bạn có thể cấu hình SSH để tự động sử dụng private key mặc định (id_rsa) nếu không chỉ định tùy chọn -i. Điều này có thể được thực hiện bằng cách chỉnh sửa file ~/.ssh/config.


    
scp: Sao chép tệp giữa máy cục bộ và máy chủ từ xa.
   
rsync: Sao chép và đồng bộ hóa tệp và thư mục.
   
tar, zip, unzip: Nén và giải nén tệp.
    
mount, umount: Gắn và tháo các phân vùng ổ đĩa.


## Xử lý và chỉnh sửa văn bản

  
    sed: Thực hiện các thao tác chỉnh sửa văn bản.
   
    sort: Sắp xếp dữ liệu.
    
    uniq: Loại bỏ các dòng trùng lặp.
   
    wc: Đếm số dòng, từ và ký tự trong văn bản.
  
    cut: Trích xuất các cột hoặc trường dữ liệu.


## Chẩn đoán và xác định vấn đề mạng


    ping/hping3: Kiểm tra kết nối mạng.
    traceroute/tracert: Hiển thị đường đi của gói tin qua các router.
    dig: Tra cứu thông tin về domain name system (DNS).
    netstat: Hiển thị thông tin về các kết nối mạng.



---
### Nguồn: [Vietnix](https://vietnix.vn/category/linux/), [Wikipedia](https://vi.wikipedia.org/wiki/Linux), .v.v.... 




### Tác giả: *Quang Huy* 
