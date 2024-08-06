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
    
- `seq=2`: Số thứ tự của gói tin ICMP trong trường hợp này đây là gói tin thứ 2 trong chuỗi.

- `ttl=53`: TTL(Time to live) là một giá trị được sử dụng để kiểm soát số lần một gói tin ***ICMP echo request*** có thể được chuyển tiếp (Forward) trước khi bị loại bỏ. Giá trị 53 Cho thấy gói tin đã đi qua 53 router trước khi đến được đích.

- `time=3.78 ms`: Đây là thời gian phản hồi, tức là thời gian gói tin ***ICMP echo reply*** đi từ máy tính nhận trở về. Trong TH này thời gian phản hồi là 3.78 ms.

> Tương tự với lệnh `hping3 --icmp vietnix.vn`

### 2. Netstat: Hiển thị thông tin về các kết nối mạng.


- Lệnh netstat (Network Statistics) là một công cụ hữu ích để hiển thị thông tin về các kết nối mạng, các socket đang lắng nghe, và các hoạt động mạng khác trên hệ thống. Dưới đây là các tùy chọn để hiển thị các socket đang lắng nghe với các yêu cầu cụ thể:

**Hiển thị các socket đang lắng nghe:**

    `netstat -l`

**OUPUT:**

    ```
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 _localdnsstub:domain    0.0.0.0:*               LISTEN     
    tcp        0      0 _localdnsproxy:domain   0.0.0.0:*               LISTEN
    ...
    ...
    Active UNIX domain sockets (only servers)
    Proto RefCnt Flags       Type       State         I-Node   Path
    unix  2      [ ACC ]     STREAM     LISTENING     13095    /tmp/.ICE-unix/1856
    unix  2      [ ACC ]     STREAM     LISTENING     11417    /tmp/.X11-unix/X0
    unix  2      [ ACC ]     STREAM     LISTENING     6490     /run/systemd io.systemd.sysext
    ...
    ...
    ```

**Không phân giải tên host:**

    `netstat --numeric-hosts`

**OUPUT:**

    ```
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 192.168.0.132:40914     91.108.56.121:443       ESTABLISHED
    tcp        0      0 192.168.0.132:41122     52.70.125.53:443        ESTABLISHED
    ...
    ...
    Active UNIX domain sockets (w/o servers)
    Proto RefCnt Flags       Type       State         I-Node   Path
    unix  3      [ ]         SEQPACKET  CONNECTED     157174   
    unix  3      [ ]         STREAM     CONNECTED     15430    
    unix  3      [ ]         STREAM     CONNECTED     14400    /run/systemd/journal/stdout
    ...
    ...
    ```

**Không phân giải tên port:**

    `netstat --numeric-ports`

**OUPUT:**

    ```
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 192.168.0.132:40914     91.108.56.121:443       ESTABLISHED
    tcp        0      0 192.168.0.132:41122     52.70.125.53:443        ESTABLISHED
    ...
    ...
    Active UNIX domain sockets (w/o servers)
    Proto RefCnt Flags       Type       State         I-Node   Path
    unix  3      [ ]         SEQPACKET  CONNECTED     157174   
    unix  3      [ ]         STREAM     CONNECTED     15430    
    unix  3      [ ]         STREAM     CONNECTED     14400    /run/systemd/journal/stdout
    ...
    ...
    ```

**Hiển thị tên/PID của tiến trình:**

    `netstat -p`

**OUPUT:**

    ```
    \(Not all processes could be identified, non-owned process info
     will not be shown, you would have to be root to see it all.)
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
    tcp        0      0 192.168.0.132:40914     91.108.56.121:https     ESTABLISHED 8908/telegram-deskt 
    tcp        0      0 192.168.0.132:41122     ec2-52-70-125-53.:https ESTABLISHED 2503/firefox        
    ...
    ...
    Active UNIX domain sockets (w/o servers)
    Proto RefCnt Flags       Type       State         I-Node   PID/Program name     Path
    unix  3      [ ]         SEQPACKET  CONNECTED     157174   8637/firefox-bin     
    unix  3      [ ]         STREAM     CONNECTED     15430    2221/xapp-sn-watche  
    unix  3      [ ]         STREAM     CONNECTED     14400    -                    /run/systemd/journal/stdout
    ...
    ...
    ```

**Chỉ hiển thị các socket TCP:**

    `netstat -t`

**OUPUT:**

    ```
    huynet@haionnet:~$ netstat -t
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 192.168.0.132:40914     91.108.56.121:https     ESTABLISHED
    tcp        0      0 192.168.0.132:41122     ec2-52-70-125-53.:https ESTABLISHED
    tcp        0      0 192.168.0.132:34662     93.243.107.34.bc.:https ESTABLISHED
    ...
    ...
    ```

**Chỉ hiển thị các socket UDP:**

    `netstat -u`

**OUPUT:**

    ```
    huynet@haionnet:~$ netstat -u
    Active Internet connections (w/o servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    udp        0      0 192.168.0.132:bootpc    192.168.0.1:bootps      ESTABLISHED
    
    ```

Kết hợp các tùy chọn trên, lệnh netstat để hiển thị các socket đang lắng ngửa với các yêu cầu cụ thể sẽ như sau:

    `netstat -lntp`

**Này sẽ hiển thị:**

- Các socket đang lắng nghe (-l)

- Không phân giải tên host và port (-n)

- Hiển thị tên/PID của tiến trình (-p)

- Chỉ hiển thị các socket TCP (-t)

Kết quả sẽ bao gồm các thông tin như địa chỉ local, địa chỉ remote, trạng thái kết nối, và PID/tên tiến trình sở hữu các socket đang lắng nghe.


### 3. ps: Hiển thị thông tin về các tiến trình đang chạy.


`ps` (process status) là lệnh dùng để hiển thị thông tin về các tiến trình đang chạy trong hệ thống Unix/Linux.

**Hiển thị danh sách tiến trình:**

    `ps`

**OUPUT:**

    ```
    huynet@haionnet:~$ ps
        PID TTY          TIME CMD
       9850 pts/0    00:00:00 bash
      10563 pts/0    00:00:00 ps
    ```

Lệnh này sẽ hiển thị danh sách các tiến trình thuộc về user hiện tại, bao gồm PID (process ID), TTY (terminal liên kết), TIME (thời gian chạy) và COMMAND (lệnh khởi chạy tiến trình).

**Hiển thị chi tiết thông tin tiến trình:**

    `ps -ef`
    
**OUPUT:**

    ```
    UID          PID    PPID  C STIME TTY          TIME CMD
    root           1       0  0 08:20 ?        00:00:01 /sbin/init splash
    root           2       0  0 08:20 ?        00:00:00 [kthreadd]
    root           3       2  0 08:20 ?        00:00:00 [pool_workqueue_release]
    ...
    huynet     10516   10487  1 08:44 ?        00:00:01 /usr/bin/xed /home/huynet/Do
    root       10634       2  0 08:46 ?        00:00:00 [kworker/3:0]
    root       10640       2  0 08:46 ?        00:00:00 [kworker/u8:1]
    huynet     10659    9850 99 08:47 pts/0    00:00:00 ps -ef
    
    ```

Lệnh này sẽ hiển thị thông tin chi tiết về tất cả các tiến trình đang chạy, bao gồm: PID, PPID (parent process ID), USER, %CPU, %MEM, VSZ (virtual memory size), RSS (resident set size) và COMMAND.

**Kill (dừng) một tiến trình:**

    `kill [PID]`

Lệnh này sẽ dừng tiến trình với PID tương ứng. Mặc định, lệnh kill sẽ gửi tín hiệu "TERM" (15) để yêu cầu tiến trình tự dừng.

Nếu tiến trình không dừng được, bạn có thể sử dụng tín hiệu "KILL" (9) mạnh mẽ hơn:

    kill -9 [PID]

**Một số tùy chọn khác của lệnh ps:**

    ps aux: Hiển thị tất cả các tiến trình của tất cả các user.
    ps -eo pid,user,comm: Hiển thị PID, user và command.
    ps -eo pid,user,%cpu,%mem,comm: Hiển thị PID, user, CPU usage, memory usage và command.

Ví dụ:

    ```
    $ ps
      PID TTY          TIME CMD
     1234 pts/0    00:00:05 bash
     5678 pts/0    00:00:01 python
     9012 pts/0    00:00:02 node
    ```

    ```
    $ ps -ef
    UID        PID  PPID  C STIME TTY          TIME CMD
    user1     1234  4321  0 10:30 pts/0    00:00:05 /bin/bash
    user1     5678  1234  0 10:32 pts/0    00:00:01 /usr/bin/python3 app.py
    user1     9012  1234  0 10:33 pts/0    00:00:02 /usr/bin/node server.js
    ```

    ```
    $ kill 5678
    $ kill -9 9012
    ```


### 4. top: Hiển thị thông tin về các tiến trình đang chạy và mức độ sử dụng tài nguyên.


`top` là một lệnh rất hữu ích trong Linux/Unix để hiển thị thông tin về các tiến trình (process) đang chạy trong hệ thống, bao gồm cả việc theo dõi việc sử dụng tài nguyên của CPU và bộ nhớ.

**Kiểm tra tài nguyên CPU của các tiến trình:**

Khi chạy lệnh top, bạn sẽ thấy một bảng thông tin về các tiến trình, bao gồm cả % CPU đang được sử dụng bởi từng tiến trình. Những tiến trình đang sử dụng nhiều CPU nhất sẽ được liệt kê ở đầu.

**RUN:**

    ```
    $ top
    top - 14:32:55 up 2 days, 12:34,  2 users,  load average: 0.15, 0.20, 0.18
    Tasks: 254 total,   1 running, 253 sleeping,   0 stopped,   0 zombie
    %Cpu(s):  3.3 us,  1.1 sy,  0.0 ni, 95.5 id,  0.1 wa,  0.0 hi,  0.0 si,  0.0 st
    KiB Mem :  8124908 total,   771748 free,  1615028 used,  5738132 buff/cache
    KiB Swap:  2097148 total,  2097148 free,        0 used.  5323436 avail Mem
    
      PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
      424 root      20   0  159208  11716   8444 S   3.3  0.1   0:01.22 systemd-journal
      465 root      20   0  268616  13572   9156 S   2.0  0.2   0:02.91 systemd-network
     1096 user1     20   0   41420   3460   3048 S   1.7  0.0   0:00.14 sshd
    ```

Trong ví dụ trên, chúng ta có thể thấy rằng CPU đang hoạt động ở mức rất nhàn nhã (95.5% idle) và không có tiến trình zombie. Các tiến trình đang sử dụng nhiều CPU nhất là systemd-journal (3.3%) và systemd-network (2.0%).


**Giải thích về các thông số quan trọng:**

- **Load average:** Đây là số trung bình của các công việc (tasks) đang chờ xử lý hoặc đang chạy trong 1, 5 và 15 phút gần đây. Số càng cao thì hệ thống càng bận.

- **us (user):** Thời gian CPU dành cho các tiến trình người dùng.
        
- **sy (system):** Thời gian CPU dành cho các tiến trình hệ thống.
        
- **ni (nice):** Thời gian CPU dành cho các tiến trình có độ ưu tiên "nice".
        
- **id (idle):** Thời gian CPU không làm gì (nhàn rỗi).
        
- **wa (wait):** Thời gian CPU phải đợi I/O.
        
- **hi (hardware interrupt):** Thời gian CPU xử lý các ngắt phần cứng.
        
- **si (software interrupt):** Thời gian CPU xử lý các ngắt phần mềm.
        
- **st (stolen time):** Thời gian CPU bị ảo hóa (virtual machines) chiếm dụng.

- **Zombie process:** Là các tiến trình đã kết thúc nhưng vẫn còn trong bảng quản lý tiến trình. Chúng cần phải được "dọn dẹp" bởi các tiến trình cha.

- **Sleeping process:** Là các tiến trình đang chờ một sự kiện nào đó (I/O, tín hiệu, v.v.) trước khi tiếp tục chạy.


### 5. free: Hiển thị thông tin về bộ nhớ.

`free` là một lệnh rất hữu ích trong Linux/Unix để hiển thị thông tin về sử dụng bộ nhớ RAM của hệ thống.

Khi chạy lệnh free, bạn sẽ thấy một bảng thông tin với các cột sau:

- **total:** Tổng dung lượng bộ nhớ RAM có sẵn trên hệ thống.

- **used:** Bộ nhớ RAM đã được sử dụng.

- **free:** Bộ nhớ RAM còn trống.

- **shared:** Bộ nhớ RAM dùng chung.

- **buff/cache:** Bộ nhớ RAM dành cho cache và buffers.

- **available:** Bộ nhớ RAM có thể sử dụng ngay lập tức (không tính cache và buffers).

Ví dụ kết quả của lệnh free:

    ```
                  total        used        free      shared  buff/cache   available
    Mem:        8124908     1615028      771748       69624     5738132     5323436
    Swap:       2097148            0     2097148
    ```

Trong ví dụ này:

- **total:** Tổng dung lượng RAM là 8GB.

- **used:** 1.6GB RAM đang được sử dụng.

- **free:** 771MB RAM còn trống.

- **shared:** 69MB RAM dùng chung.

- **buff/cache:** 5.7GB RAM dành cho cache và buffers.

- **available:** 5.3GB RAM có thể sử dụng ngay lập tức.


### 6. df: Hiển thị thông tin về dung lượng ổ đĩa.

`df` là một lệnh rất hữu ích trong Linux/Unix để hiển thị thông tin về trạng thái và sử dụng của các hệ thống tệp tin (file systems) trên hệ thống.

Khi chạy lệnh `df`, bạn sẽ thấy một bảng thông tin với các cột sau:

- **Filesystem:** Tên của hệ thống tệp tin.

- **Size:** Tổng dung lượng của hệ thống tệp tin.

- **Used:** Dung lượng đã sử dụng của hệ thống tệp tin.

- **Avail:** Dung lượng còn trống của hệ thống tệp tin.

- **Use%:** Phần trăm dung lượng đã sử dụng của hệ thống tệp tin.

- **Mounted on:** Vị trí (mount point) của hệ thống tệp tin trên hệ thống.

Ví dụ kết quả của lệnh df:

    ```
    Filesystem     Size  Used Avail Use% Mounted on
    /dev/sda1      100G   50G   45G  55% /
    tmpfs         3.9G  188M  3.7G   5% /run
    /dev/sda2      500G  460G   15G  95% /home
    ```


**Trong ví dụ này:**

- **/dev/sda1** là phân vùng chứa hệ thống tệp tin / (root) với dung lượng 100GB, đã sử dụng 50GB và còn trống 45GB.

- **tmpfs** là một hệ thống tệp tin tạm thời (in-memory) dùng để lưu trữ các tập tin tạm thời, với dung lượng 3.9GB và đang sử dụng 188MB.

- **/dev/sda2** là phân vùng chứa hệ thống tệp tin /home với dung lượng 500GB, đã sử dụng 460GB và còn trống 15GB.

- **Phân vùng /** (root) là phân vùng chứa hệ thống tệp tin chính của hệ thống Linux. 

Đây là phân vùng quan trọng nhất, chứa tất cả các tệp tin cần thiết cho việc khởi động và vận hành hệ thống. Nó thường được đặt trên ổ cứng chính (primary disk) và là phân vùng mặc định khi cài đặt Linux.


## Quản lý FILE và thư mục

### 1. cat: Hiển thị nội dung của tệp.


Lệnh `cat` trong Linux/Unix được sử dụng để:

1. **Hiển thị nội dung của một file**:
   
   ```
   cat file.txt
   ```
   
Lệnh này sẽ in ra toàn bộ nội dung của file `file.txt`.

2. **Hiển thị dòng thứ `n` trong file**:
   
   ```
   cat -n file.txt | head -n 5
   ```
   
Lệnh này sẽ in ra số thứ tự của các dòng cùng với nội dung, và chỉ hiển thị 5 dòng đầu tiên.

3. **Ghi nhiều dòng vào một file bằng cách sử dụng `EOF` (End Of File)**:

    ```
    huynet@haionnet:~$ cat > newfile.txt << EOF
    > huydang
    > danghuy
    > huydangdd
    > EOF
    ```
Lệnh này sẽ tạo một file mới có tên `new_file.txt` và ghi ba dòng văn bản vào file đó. Người dùng sẽ nhấn `Ctrl+D` để kết thúc việc nhập dữ liệu vào file.

**CHECK:**
    
    ```
    huynet@haionet:~$ cat newfile.txt 
    huydang
    danghuy
    huydangdd
    ```

**Lưu ý:**
   
- `cat > new_file.txt` mở file `new_file.txt` ở chế độ ghi (write mode).
     
- `<< EOF` và `EOF` là các chuỗi bắt đầu và kết thúc việc nhập dữ liệu vào file.

**Các tùy chọn thường dùng của lệnh `cat`:**

- `-n`: Hiển thị số thứ tự của các dòng.
- 
- `-E`: Hiển thị ký tự `$` ở cuối mỗi dòng.
- 
- `-T`: Hiển thị các ký tự TAB dưới dạng `^I`.

Lệnh `cat` rất linh hoạt và có thể kết hợp với các lệnh khác để thực hiện nhiều tác vụ như: nối nhiều file, tạo file, sửa file, v.v.


### 2. echo: In ra văn bản.


Lệnh `echo` trong Linux/Unix được sử dụng để in một chuỗi văn bản ra màn hình. Nó cũng có thể được sử dụng để thao tác với các file, bao gồm:

1. **Chèn thêm một dòng vào cuối file:**

    ```
    echo "Dòng mới" >> newfile.txt
    ```

**CHECK:**

    ```
    huynet@haionet:~$ cat newfile.txt 
    huydang
    danghuy
    huydangdd
    Dòng mới
    ```

Lệnh này sẽ thêm dòng "Dòng mới" vào cuối file `file.txt`. Nếu file không tồn tại, nó sẽ tạo ra file mới.

**Lưu ý:**
   
- Sử dụng `>>` để thêm dữ liệu vào cuối file. Nếu file không tồn tại, nó sẽ tạo ra file mới.

1. **Ghi (overwrite) nội dung của file:**
 
    ```
    echo "Nội dung mới" > file.txt
    ```

**CHECK:**

    ```
    huynet@haionet:~$ cat newfile.txt 
    Nội dung mới
    ```

Lệnh này sẽ ghi đè toàn bộ nội dung của file `file.txt` bằng chuỗi "Nội dung mới". Nếu file không tồn tại, nó sẽ tạo ra file mới.

**Lưu ý:**
   
- Sử dụng `>` để ghi đè nội dung file. Nếu file không tồn tại, nó sẽ tạo ra file mới.

***Một vài tùy chọn thường dùng của lệnh `echo`:***

- `-n`: Không in dấu newline (xuống dòng) ở cuối.
  
- `-e`: Cho phép sử dụng các ký tự đặc biệt như `\n` (newline), `\t` (tab), v.v.

Ngoài ra, lệnh `echo` cũng có thể được sử dụng để in ra các biến môi trường hoặc kết hợp với các lệnh khác như `sed`, `awk`, v.v. để thực hiện các tác vụ xử lý file nâng cao hơn.


### 3. tail/head: Hiển thị một phần nội dung của tệp.


Lệnh `tail` và `head` trong Linux/Unix được sử dụng để hiển thị một phần nội dung của file.

1. **Lệnh `tail`:**
   
- `tail file.txt`: Hiển thị 10 dòng cuối cùng của file `file.txt`.
     
- `tail -n 5 file.txt`: Hiển thị 5 dòng cuối cùng của file `file.txt`.
     
- `tail -f file.txt`: Theo dõi (follow) và hiển thị dòng mới được thêm vào cuối file `file.txt` (thường dùng để xem log files).

2. **Lệnh `head`:**
   
- `head file.txt`: Hiển thị 10 dòng đầu tiên của file `file.txt`.
     
- `head -n 5 file.txt`: Hiển thị 5 dòng đầu tiên của file `file.txt`.

3. **Sự khác biệt giữa `tail` và `tailf`:**
   
- `tail file.txt`: Hiển thị 10 dòng cuối cùng của file và sau đó dừng.
     
- `tailf file.txt`: Tương tự như `tail -f file.txt`, theo dõi và hiển thị các dòng mới được thêm vào cuối file.

**Một vài tùy chọn thường dùng của `tail` và `head`:**

- `-n`: Chỉ định số dòng cần hiển thị.
  
- `-f`: Theo dõi và hiển thị các dòng mới được thêm vào cuối file (tương tự `tailf`).
  
- `-c`: Chỉ định số byte cần hiển thị.

Lệnh `tail` và `head` rất hữu ích khi cần xem nhanh một phần nội dung của file, đặc biệt là khi làm việc với các file log. Kết hợp với các lệnh khác như `grep`, `awk`, `sed`, v.v. sẽ rất mạnh mẽ trong việc xử lý và phân tích file.


### 4. find: Tìm kiếm tệp và thư mục.


Lệnh `find` trong Unix/Linux được sử dụng để tìm kiếm các file và thư mục dựa trên các tiêu chí khác nhau.

**Tìm các file có đuôi .log:**

    `find . -type f -name "*.log"`

Lệnh này sẽ tìm các file (không phải thư mục) có tên kết thúc bằng .log trong thư mục hiện tại (và các thư mục con).

**Tìm các thư mục có tên abc:**

    `find . -type d -name "abc"`

Lệnh này sẽ tìm các thư mục có tên chính xác là abc trong thư mục hiện tại (và các thư mục con).

**Tìm các file có tên abc:**

    `find . -type f -name "abc"`

Lệnh này sẽ tìm các file (không phải thư mục) có tên chính xác là abc trong thư mục hiện tại (và các thư mục con).

**Tìm các file có tên abc và đặt chế độ read-only:**

    `find . -type f -name "abc" -exec chmod 444 {} \;`

Lệnh này sẽ tìm các file (không phải thư mục) có tên chính xác là abc trong thư mục hiện tại (và các thư mục con), sau đó đặt chế độ read-only (444) cho những file đó.

**Một số tùy chọn khác của lệnh find bao gồm:**

```
    -type [f|d]: Tìm file (f) hoặc thư mục (d)
    -name "[pattern]": Tìm theo tên file/thư mục khớp với mẫu
    -iname "[pattern]": Tìm theo tên file/thư mục khớp với mẫu, không phân biệt chữ hoa/chữ thường
    -size [+|-]N[c|k|M|G]: Tìm file có kích thước lớn hơn (+), nhỏ hơn (-) hoặc bằng N byte, kilobyte, megabyte, gigabyte
    -mtime [+|-]N: Tìm file được sửa đổi cách đây N ngày
```

Lệnh find rất mạnh mẽ và có thể được sử dụng để thực hiện nhiều tác vụ khác nhau trên các file và thư mục.


### 5. cp: Sao chép tệp.


Lệnh cp trong Unix/Linux được sử dụng để sao chép file hoặc thư mục.

**Sao chép file:**

    `cp source_file.txt destination_file.txt`

Lệnh này sẽ sao chép file source_file.txt thành destination_file.txt trong cùng thư mục.

**Sao chép thư mục:**

    `cp -r source_folder destination_folder`

Lệnh này sẽ sao chép thư mục source_folder (và tất cả nội dung bên trong) thành destination_folder. Tùy chọn -r (recursive) cho phép sao chép thư mục và toàn bộ nội dung bên trong.

**Một số tùy chọn khác của lệnh cp bao gồm:**

```
    -i: Hỏi trước khi ghi đè file đích
    -v: Hiển thị thông tin về quá trình sao chép
    -p: Giữ nguyên các thuộc tính của file (chủ sở hữu, quyền, thời gian chỉnh sửa, v.v.)
    -u: Chỉ sao chép khi file đích cũ hơn file nguồn
    -f: Ghi đè file đích mà không cần xác nhận
```

**Ví dụ:**

    `cp -i file1.txt file2.txt`

Lệnh này sẽ sao chép file1.txt thành file2.txt và hỏi trước khi ghi đè nếu file2.txt đã tồn tại.

Lệnh cp là một công cụ hữu ích khi cần sao chép file hoặc thư mục trong hệ thống tập tin.



### 6. mv: Di chuyển hoặc đổi tên tệp.


Lệnh `mv` trong Unix/Linux được sử dụng để di chuyển hoặc đổi tên file và thư mục.

**Di chuyển file:**

    `mv source_file.txt destination_folder/`

Lệnh này sẽ di chuyển file source_file.txt đến thư mục destination_folder.

**Di chuyển thư mục:**

    `mv source_folder/ destination_folder/`

Lệnh này sẽ di chuyển thư mục source_folder đến thư mục destination_folder.

**Đổi tên file:**

    `mv old_filename.txt new_filename.txt`

Lệnh này sẽ đổi tên file từ old_filename.txt thành new_filename.txt.

**Đổi tên thư mục:**

    `mv old_foldername/ new_foldername/`

Lệnh này sẽ đổi tên thư mục từ old_foldername thành new_foldername.

***Một số tùy chọn khác của lệnh mv bao gồm:***

    ```
    -i: Hỏi trước khi ghi đè file đích
    -v: Hiển thị thông tin về quá trình di chuyển
    -f: Ghi đè file đích mà không cần xác nhận
    ```

**Ví dụ:**

    `mv -i file1.txt file2.txt`

Lệnh này sẽ di chuyển file1.txt thành file2.txt và hỏi trước khi ghi đè nếu file2.txt đã tồn tại.

Lệnh mv là một công cụ rất hữu ích khi cần di chuyển hoặc đổi tên file và thư mục trong hệ thống tập tin.


### 7. rm: Xóa tệp.


Lệnh rm (remove) trong Linux/Unix được sử dụng để xóa các tệp tin và thư mục.

**Cú pháp cơ bản của lệnh rm như sau:**

    `rm [options] file(s)`

**Một số options thường dùng của lệnh rm:**

    -i: Yêu cầu xác nhận trước khi xóa mỗi tệp tin.
    -r (recursive): Xóa thư mục và tất cả nội dung bên trong.
    -f (force): Xóa mà không cần xác nhận, bỏ qua các lỗi.
    -v (verbose): Hiển thị thông báo về các tệp tin đang bị xóa.

***Ví dụ:***

**Xóa một tệp tin:**

    `rm file.txt`

**Xóa nhiều tệp tin:**

    `rm file1.txt file2.txt file3.txt`

**Xóa một thư mục và tất cả nội dung bên trong:**

    `rm -r directory/`

**Xóa một tệp tin mà không cần xác nhận:**

    `rm -f file.txt`

***Lưu ý:***

- Khi sử dụng lệnh rm, bạn cần rất cẩn thận vì các tệp tin/thư mục bị xóa sẽ không thể khôi phục.

- Có thể sử dụng lệnh rm -i để yêu cầu xác nhận trước khi xóa từng tệp tin/thư mục.

- Lệnh rmdir có thể dùng để xóa các thư mục trống.

Lệnh `rm` là một công cụ mạnh mẽ nhưng cũng rất nguy hiểm nếu sử dụng không cẩn thận, do đó cần sử dụng với sự thận trọng.


### 8. ls: Liệt kê các tệp và thư mục.


`ls` (list) là lệnh dùng để liệt kê danh sách các file và thư mục trong Unix/Linux.

**Liệt kê danh sách file/thư mục:**

    `ls`

Lệnh này sẽ liệt kê tất cả các file và thư mục trong thư mục hiện tại.

**Liệt kê danh sách file/thư mục và thuộc tính:**

    `ls -l`

**Lệnh này sẽ liệt kê thông tin chi tiết về các file và thư mục, bao gồm:**

    Quyền truy cập
    Số liên kết
    Chủ sở hữu
    Nhóm
    Kích thước
    Ngày/giờ sửa đổi
    Tên file/thư mục

**Show file ẩn:**

    `ls -a`

Lệnh này sẽ liệt kê tất cả các file và thư mục, bao gồm cả các file ẩn (bắt đầu bằng dấu chấm ".").

***Một số tùy chọn khác của lệnh ls:***

    ls -R: Liệt kê đệ quy tất cả các file và thư mục trong thư mục hiện tại và các thư mục con.
    ls -t: Sắp xếp kết quả theo thời gian sửa đổi mới nhất.
    ls -S: Sắp xếp kết quả theo kích thước file lớn nhất.

**Ví dụ:**

    ```
    $ ls
    file1.txt  file2.txt  directory1/
    ```

    ```
    $ ls -l
    -rw-r--r-- 1 user1 user1 100 Aug 5 2023 file1.txt
    -rw-r--r-- 1 user1 user1 200 Aug 5 2023 file2.txt
    drwxr-xr-x 2 user1 user1 4096 Aug 5 2023 directory1/
    ```

    ```
    $ ls -a
    .  ..  .hidden_file  file1.txt  file2.txt  directory1/
    ```

Lệnh ls cung cấp nhiều tùy chọn để liệt kê và hiển thị thông tin file/thư mục theo cách mong muốn.

### 9. chmod, chown, chattr: Thay đổi quyền và thuộc tính của tệp và thư mục.


**Phân quyền User/Group trong Unix/Linux sử dụng các lệnh sau:**

`chmod`: Thay đổi quyền truy cập của file/thư mục.

**Phân quyền bằng số:**

    `chmod 755 file.txt`

**Giải thích:**

    7 (rwx) cho chủ sở hữu
    5 (r-x) cho group
    5 (r-x) cho người dùng khác

**Phân quyền bằng chữ:**

    chmod u+x,g+rw,o+r file.txt

**Giải thích:**

        u (user): Chủ sở hữu
        g (group): Nhóm
        o (others): Người dùng khác
        + (add), - (remove), = (set)
        r (read), w (write), x (execute)

`chown`: Thay đổi chủ sở hữu (user) và nhóm (group) của file/thư mục.

    ```
    chown user:group file.txt
    chown -R user:group directory/
    ```

`chattr:` Thay đổi các thuộc tính đặc biệt của file/thư mục.

**Set Immutable Attribute (Thuộc tính không thể thay đổi):**

    `chattr +i file.txt`

**Remove Immutable Attribute:**

    `chattr -i file.txt`

***Một số thuộc tính khác của chattr:***

    a: Chỉ cho phép thêm dữ liệu vào file (append-only)
    c: File sẽ được nén tự động khi ghi
    d: File sẽ không được include trong sao lưu
    i: File/thư mục không thể bị sửa đổi (immutable)
    s: Xóa nội dung file khi xóa
    S: Ghi thay đổi đồng bộ ngay lập tức
    u: Có thể khôi phục nội dung file khi xóa

Phân quyền và quản lý quyền truy cập file/thư mục rất quan trọng để bảo mật hệ thống Unix/Linux.

### 10. ln: Tạo liên kết (symbolic link và hard link).


***Symbolic Links (Sym Link):***

**Định nghĩa:** Symbolic link (symlink) là một loại file đặc biệt, nó chứa một đường dẫn tới file/thư mục khác. Khi truy cập symlink, hệ thống sẽ tự động điều hướng đến file/thư mục đích.

**Ví dụ:**

    ln -s /path/to/target /path/to/symlink

Lệnh trên tạo một symbolic link /path/to/symlink trỏ đến file/thư mục /path/to/target.

***Hard Links:***

**Định nghĩa:** Hard link là một entry trong file system trỏ trực tiếp đến inode của file. Mỗi file có thể có nhiều hard link, và các hard link này đều trỏ đến cùng một nội dung file.

**Ví dụ:**

    `ln /path/to/target /path/to/hardlink`

Lệnh trên tạo một hard link /path/to/hardlink trỏ đến cùng inode như /path/to/target.

**Sự khác biệt giữa Symbolic Links và Hard Links:**

***Symbolic Links:***

- Là một file đặc biệt, chứa một đường dẫn tới file/thư mục đích.

- Khi truy cập symlink, hệ thống sẽ tự động điều hướng đến file/thư mục đích.

- Có thể trỏ đến file/thư mục không tồn tại.

- Khi file/thư mục đích bị xóa, symlink vẫn tồn tại nhưng không trỏ đến đâu.

***Hard Links:***
        
- Là một entry trong file system trỏ trực tiếp đến inode của file.

- Các hard link trỏ đến cùng một nội dung file.
        
- Không thể tạo hard link cho thư mục.
        
- Khi file gốc bị xóa, các hard link vẫn tồn tại và truy cập được nội dung file.

**Ví dụ:**

**Tạo symbolic link**

    `ln -s /path/to/target /path/to/symlink`

**Tạo hard link**

    `ln /path/to/target /path/to/hardlink`

Symbolic links và hard links đều có ứng dụng riêng, tuỳ thuộc vào nhu cầu của từng trường hợp cụ thể.

## Truyền FILE và sao lưu dữ liệu

### 1. SSH: Kết nối và thực hiện lệnh trên máy chủ từ xa.

***Lưu ý: Trước khi dùng ssh cần đảm bảo client-server đều đã mở port 22(`SSH`) hoặc port liên quan đên `SSH`***

***1. Lệnh SSH dùng Password:***

**Cú pháp:** 
    
    `ssh username@remote_host`
   
Ví dụ:  

    `ssh huynet@192.168.0.9`

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

**- Tạo cặp SSH key (public key và private key) trên máy tính của bạn:**

    `ssh-keygen -t rsa -b 4096`

**Thực hiện:**

![keygenSSH](https://github.com/user-attachments/assets/d1b3d535-0227-433e-9359-6d04d00d3ec9)


Lệnh này sẽ tạo ra một cặp key RSA 4096-bit, được lưu trữ mặc định trong thư mục ~/.ssh/ với tên là id_rsa (private key) và id_rsa.pub (public key).

**- Sao chép public key lên máy chủ từ xa:**

    `ssh-copy-id username@remote_host`

or

    `ssh-copy-id -i ~/PATH/id_rsa.pub username@remote_host`

**Thực hiện:**

    ```
    huydang@haionnet:~/ssh$ sudo ssh-copy-id -i /home/huydang/ssh/id_rsa.pub huynet@192.168.1.9                                                                   /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/huydang/ssh/id_rsa.pub"                                                                    /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed                                              /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys                                            
    huynet@192.168.1.9's password:                                                         Number of key(s) added: 1          Now try logging into the machine, with:   `ssh huynet@192.168.1.9` and check to make sure that only the key(s) you wanted were added.
    ```                                          

Lệnh này sẽ sao chép public key của bạn (id_rsa.pub) lên tài khoản username trên máy chủ từ xa remote_host. Sau khi thực hiện xong, public key của bạn sẽ được lưu trữ trong file ~/.ssh/authorized_keys trên máy chủ từ xa.

**- Kết nối đến máy chủ từ xa bằng SSH, sử dụng private key:**

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


- *Mở port 2222 và cho phép người khác SSH vào với cổng này, bạn cần thực hiện các bước sau:*

**Chỉnh sửa file cấu hình SSH /etc/ssh/sshd_config:**

    `sudo nano /etc/ssh/sshd_config`

**Tìm dòng chứa Port và thay đổi giá trị từ 22 sang 2222:**

    `Port 2222`

Lưu lại và thoát khỏi trình soạn thảo

**Khởi động lại dịch vụ SSH:**

    `sudo systemctl restart sshd`


***- Mở cổng 2222 trên firewall:***

Tùy thuộc vào loại firewall bạn đang sử dụng, các lệnh để mở port 2222 sẽ khác nhau. Ví dụ với ufw:

    `sudo ufw allow 2222/tcp`

**Nếu bạn sử dụng firewalld:**

    ```
    sudo firewall-cmd --permanent --add-port=2222/tcp
    sudo firewall-cmd --reload
    ```

**Cú pháp:** 
    
    `ssh -p 2222 username@remote_host`

or

    `sudo ssh -p 2222 -i /home/huydang/ssh/id_rsa huynet@192.168.1.9`
    
**Kết quả:**
   
    ```
    huydang@haionnet:~$ ssh -p 2222  huynet@192.168.1.9
    The authenticity of host '[192.168.1.9]:2222 ([192.168.1.9]:2222)' can't be established.
    ED25519 key fingerprint is SHA256:DuuytTEM/x4tcn61S2B2tj3/+P0mj/aTzyl34DstiE4.
    This key is not known by any other names.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added '[192.168.1.9]:2222' (ED25519) to the list of known hosts.
    huynet@192.168.1.9's password: 
    Last login: Sun Aug  4 22:04:57 2024 from 192.168.1.5
    
    ```
   
    
### 2. scp: Sao chép tệp giữa máy cục bộ và máy chủ từ xa.


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

*Lưu ý:*

- Bạn cần phải có quyền truy cập SSH vào máy chủ từ xa.

- Sử dụng `-r` để sao chép thư mục, không cần này khi sao chép file.
  
- Bạn có thể chỉ định đường dẫn đầy đủ hoặc đường dẫn tương đối.
  
- Nếu không chỉ định đường dẫn đích, file/thư mục sẽ được sao chép đến thư mục hiện tại của người dùng trên máy từ xa.


### 3. rsync: Sao chép và đồng bộ hóa tệp và thư mục.

`rsync` (Remote Sync) là một công cụ rất mạnh mẽ trong Linux/Unix để sao chép và đồng bộ hóa file và thư mục giữa các máy tính. Nó có nhiều tính năng nâng cao so với lệnh `scp`.

**Sao chép một file:**

    ```
    rsync file_name user@host:/destination/path
    ```

**Ví dụ:**

    ```
    rsync myfile.txt user@remote_host:/home/user/documents
    ```

Lệnh này sẽ sao chép file `myfile.txt` từ máy hiện tại đến thư mục `/home/user/documents` trên máy `remote_host`.

**Sao chép một thư mục:**

    ```
    rsync -r directory_name user@host:/destination/path
    ```

**Ví dụ:**

    ```
    rsync -r my_folder user@remote_host:/home/user/backup
    ```

Lệnh này sẽ sao chép thư mục `my_folder` (và toàn bộ nội dung bên trong) từ máy hiện tại đến thư mục `/home/user/backup` trên máy `remote_host`.

**Sao chép dincremental (chỉ sao chép những file thay đổi):**

    ```
    rsync -avz --delete source_dir user@host:destination_dir
    ```

**Ví dụ:**

    ```
    rsync -avz --delete /home/user/documents user@remote_host:/home/user/backup
    ```

Lệnh này sẽ sao chép chỉ những file thay đổi trong thư mục `documents` trên máy hiện tại đến thư mục `backup` trên máy `remote_host`. Tham số `--delete` sẽ xóa các file ở đích nếu không còn tồn tại ở nguồn.

***Một số tùy chọn thường dùng của `rsync`:***

    ```
    - `-a`: archive mode, bảo toàn các thuộc tính của file/thư mục
    - `-v`: verbose, hiển thị tiến trình sao chép
    - `-z`: nén dữ liệu để truyền nhanh hơn
    - `--delete`: xóa các file/thư mục ở đích nếu không còn ở nguồn
    ```

 
### 4. tar, zip, unzip: Nén và giải nén tệp.


Trong Linux/Unix, có 3 lệnh phổ biến dùng để nén và giải nén file:

1. **tar** (Tape ARchive):
   
**- Nén file/thư mục vào file `.tar.gz` (Gzip compressed tar archive):**
     
     ```
     tar -czf output_file.tar.gz input_file_or_directory
     ```
     
**Ví dụ:**
     
     ```
     tar -czf my_files.tar.gz documents/ photos/
     ```
     
**- Giải nén file `.tar.gz`:**
     
     ```
     tar -xzf input_file.tar.gz
     ```
     
**Ví dụ:**

     ```
     tar -xzf my_files.tar.gz
     ```

2. **zip**:
   
**- Nén file/thư mục vào file `.zip`:**

     ```
     zip -r output_file.zip input_file_or_directory
     ```

**Ví dụ:**

     ```
     zip -r my_files.zip documents/ photos/
     ```

**- Giải nén file `.zip`:**

     ```
     unzip input_file.zip
     ```

**Ví dụ:**

     ```
     unzip my_files.zip
     ```

***Các tùy chọn thường dùng:***

    `-c`: Tạo archive mới
    `-z`: Sử dụng Gzip compression
    `-x`: Extract (giải nén) archive
    `-r`: Nén/giải nén thư mục (recursive)  
    `-f`: Chỉ định tên file archive

**Ưu điểm của `tar.gz` so với `.zip`:**

- Nén tốt hơn, file đầu ra nhỏ hơn
  
- Dễ thao tác hơn, đơn giản hơn
  
- Phổ biến hơn trong hệ thống Linux/Unix

**Ưu điểm của `.zip`:**

- Tương thích với Windows, dễ dàng chia sẻ
  
- Một số tool đơn giản hơn khi giải nén

### 5. mount, umount: Gắn và tháo các phân vùng ổ đĩa.


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



## Xử lý và chỉnh sửa văn bản

  
### 1. sed: Thực hiện các thao tác chỉnh sửa văn bản.


**Không sử dụng -i**

    `sed 's/old/new/g' file.txt`

**Kết quả sẽ in ra màn hình, file gốc không bị thay đổi**

**Sử dụng -i**

    `sed -i 's/old/new/g' file.txt`

**Nội dung file.txt sẽ được thay đổi trực tiếp**

Sử dụng -i là rất hữu ích khi cần thực hiện thay đổi trực tiếp nội dung file, nhưng cần lưu ý và tạo bản sao dự phòng trước khi thực hiện, để tránh mất dữ liệu do vô tình ghi đè.

Khi không sử dụng -i, ta có thể kiểm tra kết quả trước khi quyết định ghi vào file gốc, đây là cách an toàn hơn khi làm việc với các tập tin quan trọng.


### 2. sort: Sắp xếp dữ liệu.

Lệnh sort trong Unix/Linux được sử dụng để sắp xếp dữ liệu theo thứ tự tăng dần hoặc giảm dần. Dưới đây là các ví dụ về cách sử dụng lệnh sort:

**Sắp xếp theo thứ tự tăng dần:**

    `sort file.txt`

Lệnh này sẽ sắp xếp các dòng trong file file.txt theo thứ tự tăng dần.

**Sắp xếp theo thứ tự giảm dần:**

    `sort -r file.txt`

Lệnh này sẽ sắp xếp các dòng trong file file.txt theo thứ tự giảm dần.

**Sắp xếp theo cột:**

    `sort -k [column_number] file.txt`

Lệnh này sẽ sắp xếp các dòng trong file file.txt theo cột chỉ định, với [column_number] là số thứ tự của cột (bắt đầu từ 1).

**Ví dụ:**

    sort -k 2 file.txt

Lệnh này sẽ sắp xếp các dòng trong file file.txt theo cột thứ 2.

***Một số tùy chọn khác của lệnh sort bao gồm:***

    -n: Sắp xếp theo giá trị số
    -h: Sắp xếp các giá trị theo dạng human-readable (ví dụ: 1K, 2M, 3G)
    -f: Không phân biệt chữ hoa/chữ thường
    -t: Chỉ định ký tự phân cách giữa các trường

**Ví dụ:**

    `sort -k 2 -n file.txt`

Lệnh này sẽ sắp xếp các dòng trong file file.txt theo cột thứ 2, theo thứ tự tăng dần và xem các giá trị trong cột đó là số.

### 3. uniq: Loại bỏ các dòng trùng lặp.


Lệnh `uniq` trong Unix/Linux được sử dụng để lọc ra các dòng lặp lại trong một file.

**Lọc ra các dòng lặp lại trong một file:**

    `uniq file.txt`

Lệnh này sẽ in ra các dòng duy nhất, loại bỏ các dòng trùng lặp.

**Lọc ra các dòng lặp lại trong file và đếm số lượng các dòng lặp lại:**

    `uniq -c file.txt`

Lệnh này sẽ in ra các dòng duy nhất, và đếm số lần xuất hiện của mỗi dòng.

**Kết quả sẽ hiển thị theo định dạng:**

    [số lần xuất hiện] [dòng văn bản]

***Một số tùy chọn khác của lệnh uniq bao gồm:***

    -i: Không phân biệt chữ hoa/chữ thường
    -d: Chỉ in ra các dòng lặp lại
    -u: Chỉ in ra các dòng không lặp lại
    -f [N]: Bỏ qua N trường đầu tiên khi so sánh
    -s [N]: Bỏ qua N ký tự đầu tiên khi so sánh

**Ví dụ:**

    `uniq -c -i file.txt`

Lệnh này sẽ lọc ra các dòng lặp lại trong file file.txt, không phân biệt chữ hoa/chữ thường, và đếm số lượng các dòng lặp lại.


### 4. wc: Đếm số dòng, từ và ký tự trong văn bản.

Lệnh `wc` (Word Count) trong Unix/Linux được sử dụng để đếm số dòng, số từ và số ký tự trong một file.

**Đếm số dòng trong file:**

    `wc -l file.txt`

Lệnh này sẽ in ra số dòng trong file file.txt.

**Đếm số ký tự trong file:**

    `wc -c file.txt`

Lệnh này sẽ in ra số ký tự trong file file.txt.

***Một số tùy chọn khác của lệnh wc bao gồm:***

    -w: Đếm số từ
    -m: Đếm số ký tự (bao gồm cả khoảng trắng)
    -L: In ra chiều dài của dòng dài nhất

**Ví dụ:**

    `wc -l -c file.txt`

Lệnh này sẽ in ra cả số dòng và số ký tự trong file file.txt.

**Kết quả sẽ hiển thị theo định dạng:**

    [số dòng] [số từ] [số ký tự] [tên file]

Lệnh `wc` là một công cụ hữu ích khi cần nhanh chóng kiểm tra thông tin cơ bản về một file văn bản.


### 5. cut: Trích xuất các cột hoặc trường dữ liệu.

Lệnh `cut` trong Unix/Linux được sử dụng để trích xuất các phần cụ thể từ một dòng văn bản hoặc file.

**Trích xuất kí tự thứ n trong một chuỗi:**

    `cut -c n file.txt`

Lệnh này sẽ trích xuất kí tự thứ n từ mỗi dòng trong file file.txt.

**Trích xuất từ kí tự thứ n trở về sau:**

    `cut -c n- file.txt`

Lệnh này sẽ trích xuất từ kí tự thứ n đến cuối mỗi dòng trong file file.txt.

**Trích xuất từ kí tự thứ n trở về trước:**

    `cut -c -n file.txt`
    
Lệnh này sẽ trích xuất từ đầu mỗi dòng đến kí tự thứ n trong file file.txt.

**Ngoài ra, bạn cũng có thể sử dụng lệnh cut để trích xuất các trường dữ liệu theo dấu phân cách (như dấu phẩy, tab, v.v.):**

    `cut -d',' -f2,4 file.csv`

Lệnh này sẽ trích xuất trường thứ 2 và 4 (tính từ 1) từ mỗi dòng trong file file.csv, sử dụng dấu phẩy (,) làm dấu phân cách.

Lệnh cut rất hữu ích khi cần trích xuất thông tin cụ thể từ các file văn bản hoặc bảng dữ liệu.


## Chẩn đoán và xác định vấn đề mạng

### 1. traceroute/tracert: Hiển thị đường đi của gói tin qua các router.


Lệnh `traceroute` (hoặc tracert trên Windows) là một công cụ hữu ích để xác định đường đi của gói tin từ máy tính nguồn đến một địa chỉ IP hoặc tên miền đích. Nó cung cấp thông tin chi tiết về các bước trung gian (hop) mà gói tin phải trải qua trên đường đến đích.

- **Khi chạy lệnh traceroute, kết quả trả về sẽ bao gồm các thông tin sau:**

- **Hop Number:** Thứ tự của các bước trung gian (hop) mà gói tin phải trải qua.

- **Router IP Address:** Địa chỉ IP của mỗi router trung gian.

- **Response Time:** Thời gian (tính bằng milli giây) mà gói tin cần để đến và trở về từ mỗi hop.

- **Host Name (nếu có):** Tên miền của mỗi router trung gian, nếu có thể phân giải được.

**Ví dụ kết quả traceroute:**

    ```
    traceroute to example.com (93.184.216.34), 30 hops max, 60 byte packets
     1  192.168.1.1 (192.168.1.1)  1.234 ms  2.345 ms  1.567 ms
     2  10.0.0.1 (10.0.0.1)  5.678 ms  4.321 ms  6.789 ms
     3  192.168.0.1 (192.168.0.1)  10.012 ms  9.876 ms  11.234 ms
     4  192.168.2.1 (192.168.2.1)  12.345 ms  13.456 ms  14.567 ms
     5  example-router.isp.net (172.16.0.1)  15.678 ms  16.789 ms  17.012 ms
     6  example-border-router.isp.net (192.168.3.1)  18.345 ms  19.456 ms  20.567 ms
     7  example.com (93.184.216.34)  21.678 ms  22.789 ms  23.012 ms
    ```

**Giải thích kết quả:**

- Gói tin bắt đầu từ địa chỉ IP 192.168.1.1 ở hop đầu tiên, với thời gian phản hồi khoảng 1-2 ms.

- Tiếp theo, gói tin đi qua địa chỉ IP 10.0.0.1 ở hop thứ 2, với thời gian phản hồi khoảng 4-6 ms.

- Các hop tiếp theo là 192.168.0.1, 192.168.2.1, example-router.isp.net và example-border-router.isp.net, với thời gian phản hồi tăng dần.

- Cuối cùng, gói tin đến được địa chỉ IP 93.184.216.34 của trang web example.com, với thời gian phản hồi khoảng 21-23 ms.

### 2. dig: Tra cứu thông tin về domain name system (DNS)

Lệnh `dig` (Domain Information Groper) trong Unix/Linux được sử dụng để kiểm tra và truy vấn thông tin về các record DNS (Domain Name System).

**Kiểm tra record A, MX, NS:**

    ```
    dig example.com A
    dig example.com MX
    dig example.com NS
    ```

Các lệnh trên sẽ truy vấn và hiển thị các record A (địa chỉ IP), MX (mail server) và NS (name server) của domain example.com.

**Kiểm tra record A, MX, NS với custom DNS:**
    
    ```
    dig @8.8.8.8 example.com A
    dig @8.8.8.8 example.com MX
    dig @8.8.8.8 example.com NS
    ```

Các lệnh trên sẽ sử dụng DNS server 8.8.8.8 (Google DNS) để truy vấn các record của domain example.com.

**Một số tùy chọn khác của lệnh dig:**

    -t: Chỉ định loại record cần truy vấn (A, MX, NS, CNAME, etc.)
    -x: Thực hiện truy vấn ngược (từ IP sang domain)
    -p: Chỉ định cổng DNS (mặc định là 53)
    -s: Chỉ định file chứa các câu lệnh dig cần thực hiện
    -f: Chỉ định file chứa các domain cần truy vấn

**Ví dụ:**

    ```
    dig -t CNAME example.com
    dig -x 8.8.8.8
    dig @8.8.8.8 -p 5353 example.com
    dig -f domains.txt
    ```

Lệnh `dig` là một công cụ rất hữu ích để kiểm tra và debug các vấn đề liên quan đến DNS.

---
### Nguồn: [Vietnix](https://vietnix.vn/category/linux/), [Wikipedia](https://vi.wikipedia.org/wiki/Linux), .v.v.... 


### Tác giả: *Quang Huy* 
