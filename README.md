# Kiến thức cơ bản LINUX LP1 - Vietnix

[Kiểm tra và giám sát hệ thống](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#ki%E1%BB%83m-tra-v%C3%A0-gi%C3%A1m-s%C3%A1t-h%E1%BB%87-th%E1%BB%91ng)

[Quản lý FILE và thư mục](https://github.com/lamianguyen99/fudamental2-vietnix/tree/main?tab=readme-ov-file#qu%E1%BA%A3n-l%C3%BD-file-v%C3%A0-th%C6%B0-m%E1%BB%A5c)

[Truyền FILE và sao lưu dữ liệu](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#truy%E1%BB%81n-file-v%C3%A0-sao-l%C6%B0u-d%E1%BB%AF-li%E1%BB%87u)

[Xử lý và chỉnh sửa văn bản](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#x%E1%BB%AD-l%C3%BD-v%C3%A0-ch%E1%BB%89nh-s%E1%BB%ADa-v%C4%83n-b%E1%BA%A3n)

[Chẩn đoán và xác định vấn đề mạng](https://github.com/lamianguyen99/fudamental2-vietnix?tab=readme-ov-file#ch%E1%BA%A9n-%C4%91o%C3%A1n-v%C3%A0-x%C3%A1c-%C4%91%E1%BB%8Bnh-v%E1%BA%A5n-%C4%91%E1%BB%81-m%E1%BA%A1ng)

---

## Kiểm tra và giám sát hệ thống

    
### 1. Ping/hping3: Kiểm tra kết nối mạng.

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

### 2. Netstat: Hiển thị thông tin về các kết nối mạng.



### 3. ps: Hiển thị thông tin về các tiến trình đang chạy.
    
### 4. top: Hiển thị thông tin về các tiến trình đang chạy và mức độ sử dụng tài nguyên.
    
### 5. free: Hiển thị thông tin về bộ nhớ.

### 6. df: Hiển thị thông tin về dung lượng ổ đĩa.


## Quản lý FILE và thư mục

### 1. cat: Hiển thị nội dung của tệp.
    
### 2. echo: In ra văn bản.
    
### 3. tail/head: Hiển thị một phần nội dung của tệp.
   
### 4. find: Tìm kiếm tệp và thư mục.
   
### 5. cp: Sao chép tệp.
   
### 6. mv: Di chuyển hoặc đổi tên tệp.
   
### 7. rm: Xóa tệp.
    
### 8. ls: Liệt kê các tệp và thư mục.
   
### 9. chmod, chown, chattr: Thay đổi quyền và thuộc tính của tệp và thư mục.
    
### 10. ln: Tạo liên kết (symbolic link và hard link).



## Truyền FILE và sao lưu dữ liệu


### 1. SSH: Kết nối và thực hiện lệnh trên máy chủ từ xa.

***Lưu ý: Trước khi dùng ssh cần đảm bảo client-server đều đã mở port 22(`SSH`) hoặc port liên quan đên `SSH`***

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
huynet@192.168.1.9's password:                                                         Number of key(s) added: 1          Now try logging into the machine, with:   `ssh huynet@192.168.1.9` and check to make sure that only the key(s) you wanted were added.
```                                          

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

***3. Lệnh SSH dùng port custom:***

Cũng giống 2 cách trên, nhưng nếu remote host dùng port khác chẳng han `2222` để cho dịch vụ `SSH` thì ta sẽ cần điều chỉnh port remote như sau

```
Mở port 2222 và cho phép người khác SSH vào với cổng này, bạn cần thực hiện các bước sau:

    Chỉnh sửa file cấu hình SSH /etc/ssh/sshd_config:

sudo nano /etc/ssh/sshd_config

Tìm dòng chứa Port và thay đổi giá trị từ 22 sang 2222:

Port 2222

Lưu lại và thoát khỏi trình soạn thảo.

    Khởi động lại dịch vụ SSH:

sudo systemctl restart sshd

    Mở cổng 2222 trên firewall:

Tùy thuộc vào loại firewall bạn đang sử dụng, các lệnh để mở port 2222 sẽ khác nhau. Ví dụ với ufw:

sudo ufw allow 2222/tcp

Nếu bạn sử dụng firewalld:

sudo firewall-cmd --permanent --add-port=2222/tcp
sudo firewall-cmd --reload

```

**Cú pháp:** 
    
    `ssh -p 2222 username@remote_host`

or

    `sudo ssh -p 2222 -i /home/huydang/ssh/id_rsa huynet@192.168.1.9`
    
**Kết quả:**
   
```
huydang@huynet-vnx:~$ ssh -p 2222  huynet@192.168.1.9
The authenticity of host '[192.168.1.9]:2222 ([192.168.1.9]:2222)' can't be established.
ED25519 key fingerprint is SHA256:DuuytTEM/x4tcn61S2B2tj3/+P0mj/aTzyl34DstiE4.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[192.168.1.9]:2222' (ED25519) to the list of known hosts.
huynet@192.168.1.9's password: 
Last login: Sun Aug  4 22:04:57 2024 from 192.168.1.5

```
   
    
### 2. scp: Sao chép tệp giữa máy cục bộ và máy chủ từ xa.

RAW:

```
`scp` (Secure Copy) là một lệnh trong Linux/Unix dùng để sao chép file hoặc thư mục giữa các máy tính thông qua kết nối SSH.

**Sao chép một file:**

```
scp file_name user@host:/destination/path
```

Ví dụ:
```
scp myfile.txt user@remote_host:/home/user/documents
```
Lệnh này sẽ sao chép file `myfile.txt` từ máy hiện tại đến thư mục `/home/user/documents` trên máy `remote_host`.

**Sao chép một thư mục:**

```
scp -r directory_name user@host:/destination/path
```

Ví dụ:
```
scp -r my_folder user@remote_host:/home/user/backup
```
Lệnh này sẽ sao chép thư mục `my_folder` (và toàn bộ nội dung bên trong) từ máy hiện tại đến thư mục `/home/user/backup` trên máy `remote_host`.

Lưu ý:
- Bạn cần phải có quyền truy cập SSH vào máy chủ từ xa.
- Sử dụng `-r` để sao chép thư mục, không cần này khi sao chép file.
- Bạn có thể chỉ định đường dẫn đầy đủ hoặc đường dẫn tương对.
- Nếu không chỉ định đường dẫn đích, file/thư mục sẽ được sao chép đến thư mục hiện tại của người dùng trên máy từ xa.
```



### 3. rsync: Sao chép và đồng bộ hóa tệp và thư mục.

RAW: 

```
`rsync` (Remote Sync) là một công cụ rất mạnh mẽ trong Linux/Unix để sao chép và đồng bộ hóa file và thư mục giữa các máy tính. Nó có nhiều tính năng nâng cao so với lệnh `scp`.

**Sao chép một file:**

```
rsync file_name user@host:/destination/path
```

Ví dụ:
```
rsync myfile.txt user@remote_host:/home/user/documents
```
Lệnh này sẽ sao chép file `myfile.txt` từ máy hiện tại đến thư mục `/home/user/documents` trên máy `remote_host`.

**Sao chép một thư mục:**

```
rsync -r directory_name user@host:/destination/path
```

Ví dụ: 
```
rsync -r my_folder user@remote_host:/home/user/backup
```
Lệnh này sẽ sao chép thư mục `my_folder` (và toàn bộ nội dung bên trong) từ máy hiện tại đến thư mục `/home/user/backup` trên máy `remote_host`.

**Sao chép dincremental (chỉ sao chép những file thay đổi):**

```
rsync -avz --delete source_dir user@host:destination_dir
```

Ví dụ:
```
rsync -avz --delete /home/user/documents user@remote_host:/home/user/backup
```
Lệnh này sẽ sao chép chỉ những file thay đổi trong thư mục `documents` trên máy hiện tại đến thư mục `backup` trên máy `remote_host`. Tham số `--delete` sẽ xóa các file ở đích nếu không còn tồn tại ở nguồn.

Một số tùy chọn thường dùng của `rsync`:
- `-a`: archive mode, bảo toàn các thuộc tính của file/thư mục
- `-v`: verbose, hiển thị tiến trình sao chép
- `-z`: nén dữ liệu để truyền nhanh hơn
- `--delete`: xóa các file/thư mục ở đích nếu không còn ở nguồn
```

 
### 4. tar, zip, unzip: Nén và giải nén tệp.

RAW:

```
Trong Linux/Unix, có 3 lệnh phổ biến dùng để nén và giải nén file:

1. **tar** (Tape ARchive):
   - Nén file/thư mục vào file `.tar.gz` (Gzip compressed tar archive):
     ```
     tar -czf output_file.tar.gz input_file_or_directory
     ```
     Ví dụ:
     ```
     tar -czf my_files.tar.gz documents/ photos/
     ```
   - Giải nén file `.tar.gz`:
     ```
     tar -xzf input_file.tar.gz
     ```
     Ví dụ: 
     ```
     tar -xzf my_files.tar.gz
     ```

2. **zip**:
   - Nén file/thư mục vào file `.zip`:
     ```
     zip -r output_file.zip input_file_or_directory
     ```
     Ví dụ:
     ```
     zip -r my_files.zip documents/ photos/
     ```
   - Giải nén file `.zip`:
     ```
     unzip input_file.zip
     ```
     Ví dụ:
     ```
     unzip my_files.zip
     ```

Các tùy chọn thường dùng:
- `-c`: Tạo archive mới
- `-z`: Sử dụng Gzip compression
- `-x`: Extract (giải nén) archive
- `-r`: Nén/giải nén thư mục (recursive)
- `-f`: Chỉ định tên file archive

Ưu điểm của `tar.gz` so với `.zip`:
- Nén tốt hơn, file đầu ra nhỏ hơn
- Dễ thao tác hơn, đơn giản hơn
- Phổ biến hơn trong hệ thống Linux/Unix

Ưu điểm của `.zip`:
- Tương thích với Windows, dễ dàng chia sẻ
- Một số tool đơn giản hơn khi giải nén

Tùy vào mục đích sử dụng mà bạn có thể lựa chọn định dạng nén phù hợp.
```

### 5. mount, umount: Gắn và tháo các phân vùng ổ đĩa.

RAW:

```

Để làm những việc đó, bạn có thể sử dụng các lệnh sau:

1. **Thêm ổ cứng sdb khoảng 5GB:**
   - Giả sử ổ cứng mới được thêm vào có tên là `sdb`
   - Đầu tiên, bạn cần phải tạo phân vùng và định dạng filesystem trên ổ `sdb`:
     ```
     # Tạo phân vùng
     fdisk /dev/sdb
     
     # Định dạng filesystem (ví dụ ext4)
     mkfs.ext4 /dev/sdb1
     ```

2. **Kiểm tra số lượng ổ cứng trên máy chủ:**
   ```
   # Liệt kê tất cả các ổ cứng đã được gắn
   lsblk
   ```
   Kết quả sẽ hiển thị danh sách các ổ cứng, chẳng hạn:
   ```
   NAME   SIZE TYPE MOUNTPOINT
   sda    100G Disk 
   ├─sda1  50G Part /
   └─sda2  50G Part [SWAP]
   sdb     5G Disk
   ```

3. **Mount ổ cứng `/dev/sdb1` vào `/mnt/test`:**
   ```
   # Tạo thư mục mount point
   mkdir /mnt/test
   
   # Mount ổ cứng
   mount /dev/sdb1 /mnt/test
   ```

4. **Unmount ổ cứng `/mnt/test`:**
   ```
   # Unmount ổ cứng
   umount /mnt/test
   ```

Các lưu ý:
- Lệnh `lsblk` sẽ liệt kê tất cả các ổ cứng được gắn vào hệ thống, bao gồm cả các phân vùng.
- `fdisk` được dùng để tạo phân vùng trên ổ cứng mới.
- `mkfs.ext4` được dùng để định dạng phân vùng với filesystem ext4.
- `mount` được dùng để gắn một phân vùng vào một thư mục mount point.
- `umount` được dùng để ngắt kết nối (unmount) một phân vùng.

Sau khi mount, bạn có thể sử dụng ổ cứng `/dev/sdb1` như một thư mục bình thường tại `/mnt/test`.

```


## Xử lý và chỉnh sửa văn bản

  
### 1. sed: Thực hiện các thao tác chỉnh sửa văn bản.
   
### 2. sort: Sắp xếp dữ liệu.
    
### 3. uniq: Loại bỏ các dòng trùng lặp.
   
### 4. wc: Đếm số dòng, từ và ký tự trong văn bản.
  
### 5. cut: Trích xuất các cột hoặc trường dữ liệu.


## Chẩn đoán và xác định vấn đề mạng

### 1. traceroute/tracert: Hiển thị đường đi của gói tin qua các router.

### 2. dig: Tra cứu thông tin về domain name system (DNS)

---
### Nguồn: [Vietnix](https://vietnix.vn/category/linux/), [Wikipedia](https://vi.wikipedia.org/wiki/Linux), .v.v.... 




### Tác giả: *Quang Huy* 
