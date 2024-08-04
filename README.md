# Kiến thưc cơ bản- Vietnix

[SSL](https://vietnix.vn/ssl-la-gi/)

[Domain](https://vietnix.vn/domain-la-gi/)

[Mail Server](https://vietnix.vn/mail-server-la-gi/)

[DNS](https://vietnix.vn/dns-la-gi/)

---
## SSL


Đa phần người dùng sẽ ngừng truy cập nếu được thông báo kết nối không an toàn. Đặc biệt đối với các website `thương mại điện tử`, việc không bảo mật sẽ khiến doanh nghiệp đánh mất lượng lớn khách hàng tiềm năng và doanh thu về. Chính vì thế, chứng chỉ SSL trở nên vô cùng quan trọng.

### 1. SSL là gì ?

SSL (Secure Sockets Layer) là một [giao thức](https://vietnix.vn/protocol-la-gi/) bảo mật được sử dụng để tạo kết nối an toàn giữa `trình duyệt web` và `máy chủ web`. Nó mã hóa dữ liệu truyền giữa client và server, đảm bảo rằng thông tin không bị đánh cắp hoặc can thiệp bởi bên thứ ba. Hiện nay, SSL được xem là tiêu chuẩn bảo mật cho đa số website trên thế giới, giúp dữ liệu truyền đi trên `Internet` được bảo vệ một cách an toàn.

SSL được `Netscape` phát triển lần đầu vào năm 1995. Với mục đích đảm bảo quyền riêng tư, xác thực toàn vẹn dữ liệu trong truyền thông `Internet`. 

SSL có các phiên bản 1.0, 2.0, 3.0 nhưng các phiên bản này đã bị tìm thấy [lỗ hổng bảo mật](https://vietnix.vn/lo-hong-bao-mat/) và không còn được sử dụng nữa.

Năm 1999, SSL đã được cập nhật để trở thành [TLS](https://vietnix.vn/tls-la-gi/) ( Transport Layer Security) 

TLS có các phiên bản 1.0, 1.1, 1.2 và 1.3 trong đó TLS 1.2 và 1.3 là các phiên bản được sử dụng rộng rãi hiện nay.

### 2. Có bao nhiêu cách chứng thực SSL ?

Có 2 cách chứng thực SSL chính:

- Chứng thực bởi Tổ chức Chứng nhận (Certificate Authority - `CA`): Các tổ chức như `Let's Encrypt`, `DigiCert` , `GoDaddy`, v.v. cung cấp và quản lý các chứng chỉ SSL.
 
- Chứng thực sử dụng chứng chỉ tự ký (`self-signed certificate`): Người dùng tự tạo và ký chứng chỉ SSL cho miền của mình.


### 3. CSR file dùng làm gì trong quá trình tạo SSL?

CSR (`Certificate Signing Request`) : Đây là một đoạn text chứa thông tin của chủ sở hữu tên miền được mã hóa(gồm thông tin máy chủ, tên miền và thông tin xác thực khác). Thông tin này sẽ được dùng để gửi đến nhà cung cấp dịch vụ SSL để xác nhận.

### 4. Sử dụng OpenSSL để gen file CSR sau đó request SSL cho domain `tech.training.vietnix.tech`

Để tạo CSR file sử dụng OpenSSL cho domain `tech.training.vietnix.tech`, bạn có thể sử dụng lệnh sau:

   ```
   openssl req -new -newkey rsa:2048 -nodes -keyout tech.training.vietnix.tech.key -out tech.training.vietnix.tech.csr
   ```

Trong đó:

`openssl req -new`: Lệnh này yêu cầu OPENSSL tạo một Certificate Signing Request(CSR) mới.

`-newkey rsa:2048`: Tùy chọn này chỉ định việc tạo một khóa RSA(`Private key`) mới có độ dài 2048 bits. Độ dài khóa 2048 bits là khuyến nghị hiện nay để đảm bảo an toàn.

`-nodes`: Tùy chọn này chỉ định rằng private key không cần được mã hóa bằng mật khẩu. Điều này tiện cho việc sử dụng khóa mà không cần nhập mật khẩu thuận tiện cho việc tự động hóa backup, restore. 

- Điều này thường được cân nhắc khi sử dụng khóa ở các hệ thống an toàn và được quản lý tốt. Nếu muốn mã hóa khóa riêng chỉ cần bỏ tùy chọn  `-nodes` và nhập mật khẩu an toàn sau khi thực hiện câu lệnh trên.

`-keyout tech.training.vietnix.key` : Tùy chọn này chỉ định tệp tin để lưu trữ khóa riêng (private key) được tạo ra. Trong trường hợp này, tệp tin sẽ có tên `tech.training.vietnix.tech.key`.

`-out tech.training.vietnix.tech.csr`: Tùy chọn này chỉ định tệp tin để lưu trữ Certificate Signing Request(CSR) được tạo ra. Trong trường hợp này, tệp tin sẽ có tên `tech.training.vietnix.tech.csr`.

   Khi chạy lệnh này, OPENSSL sẽ yêu cầu bạn nhập một số thông tin về chứng chỉ như: tên, quốc gia, tiểu bang, thành phố, tên cty, tên bộ phận, tên miền. Sau khi nhập đầy đủ thông tin OPENSSL sẽ tạo ra 2 file như trên.


Sau đó, bạn có thể gửi file CSR (tech.training.vietnix.tech.csr) đến CA để yêu cầu cấp chứng chỉ SSL.

Các bước thực hiện như sau:

1. Truy cập vào trang web của CA(ví dụ Let's Encrypt, DigiCert, Comodo,v..v...) và chọn tùy chọn "Yêu cầu chứng chỉ mới".

2. Tải file CSR `tech.training.vietnix.tech.csr` lên và cung cấp các thông tin cần thiết khác như tên miền, thông tin tổ chức,v.v...

3. Thực hiện các bước thanh toán khác (nếu cần) và chờ CA xử lý yêu cầu.

4. Khi CA cấp chứng chỉ, bạn sẽ được cung cấp file chứng chỉ(Thường có đuôi .crt hoặc .pem).

Với 2 bước này, bạn đã tạo được file CSR và yêu cầu chứng chỉ SSL cho domain `tech.training.vietnix.tech`  để cài đặt chứng chỉ SSL trên máy chủ web.



### 5. Pem file là gì ?

Định dạng file phổ biến để lưu trữ và trao đổi các thông tin bảo mật như: Chứng chỉ số (digital certificates), khóa công khai(public keys), và khóa riêng (private keys). 

Các file PEM thường được bắt đầu và kết thúc bằng các dòng chữ như: `-----BEGIN CERTIFICATE-----` và `-----END CERTIFICATE-----`.

Dữ liệu trong file PEM được mã hóa bằng Base64, có thể đọc và chỉnh sửa bằng trình soạn thảo văn bản thông thường.

Khi trình duyệt kết nối với 1 website sử dụng SSL/TLS, website sẽ cung cấp một chứng chỉ số(digital certificate) để xác thực danh tính của nó.

Chứng chỉ số này chứa thông tin như tên miền, tổ chức phát hành, khóa công khai, v.v..

Để cài đặt chứng chỉ SSL/TLS trên máy chủ website, cần có 3 file chính: 
 
1. Certificate file (.crt/.pem): chứa `chứng chỉ số` của website tự ký hoặc được CA cấp.

2. Private key file(.key/.pem) chứa `private key` để mã hóa/giải mã dữ liệu.

3. CA Bundle file (.pem): Chứa chuỗi chứng chỉ `CA trung gian` để xác thực chuỗi tin cậy của chứng chỉ CA ban đầu.


ĐĂNG KÝ SSL/TLS cũng giống như bạn đi đăng ký giấy kết hôn:
```
Private key: Giấy đăng ký kết hôn gồm những thông tin của bạn.
Public key : Con dấu xác nhận của cơ quan địa phương.
CA ban đầu : Xác nhận của cơ quan địa phương.
Bundle CA  : Xác nhận của các tổ chức, cơ quan cấp cao về sự hợp lệ của cơ quan địa phương.
```


### 6. Private key ssl là gì ?

Private key là một phần quan trọng của hệ thống bảo mật SSL/TLS, được sử dụng để tạo ra kết nối an toàn giữa người dùng và máy chủ trên Internet.

Ứng dụng của private key:

- Được sử dụng để mã hóa tạo ra chữ ký số, xác nhận rằng máy chủ sở hữu chứng chỉ ssl hợp lệ.

- Khi người dùng truy cập trang website, trình duyện sẽ sử dụng private key trong chứng chỉ SSL để xác minh chữ ký số do private key tạo ra.

- Được sử dụng để mã hóa dữ liệu được truyền giữa người dùng va máy chủ.

- Điều này giúp bảo vệ thông tin nhạy cảm như thông tin thanh toán, đăng nhập.vv..v.. khỏi bị đánh cắp.

- Private key được sử dụng để giải mã dữ liệu được mã hóa bằng public key.

- Điều này đảm bảo rằng chỉ máy chử sở hữu private key mới có thể đọc đươc thông tin.

Private key được tạo ra từ việc sử dụng các thuật toán mã hóa như RSA, ECC.v.v...


> Các bước xác thực khi truy cập trang web:
> 
> 1. Người dùng truy cập vào trang web. Gửi một Request lên gồm URL trang web, HTTP headers (trình duyệt, hệ điều hành cảu người dùng), IP người dùng.
> 
> 2. Trang web thu thập các thông tin cần thiết như nội dung trang, thời gian, thông tin về kết nối, thông tin người dùng.
> 
> 3. Trang web sử dụng các thông tin này rồi dùng `private key` để mã hóa tạo ra một `chữ ký số`.
> 
> 4. Trang web gửi `dữ liệu` cùng với `chữ ký số` đến người dùng.
> 
> 5. Người dùng sử dụng `public key` để giải mã chữ ký số.
> 
> 6. Sau khi giải mã, nếu dữ liệu giải mã khớp với dữ liệu được gửi từ trang web, thì người dùng có thể xác định rằng dữ liệu là hợp lệ, chưa bị thay đổi.


### 7. PFX file là gì ? Cách chuyển từ file crt file sang PFX file.

7. PFX (Personal Information Exchange) file là một `định dạng tập tin` chứa `chứng chỉ SSL` và `khóa riêng tư` trong một tập tin duy nhất. Nó thường được sử dụng trong các ứng dụng Windows. Để chuyển từ file CRT sang PFX, bạn có thể sử dụng lệnh sau:

   ```
   openssl pkcs12 -export -in tech.training.vietnix.tech.crt -inkey tech.training.vietnix.tech.key -out tech.training.vietnix.tech.pfx
   ```
   
1. `openssl`: Đây là công cụ command-line để làm việc với các chứng chỉ SSL/TLS, mã hóa và các công nghệ liên quan.

2. `pkcs12`: Đây là một định dạng tệp tin chứa các thông tin về chứng chỉ và khóa riêng. Nó thường được sử dụng để đóng gói chứng chỉ và khóa riêng vào một tệp tin duy nhất.

3. `-export`: Tùy chọn này cho biết rằng chúng ta muốn xuất (export) các thông tin từ chứng chỉ và khóa riêng vào tệp tin PKCS12.

4. `-in tech.training.vietnix.tech.crt`: Đây là đường dẫn của tệp tin chứng chỉ SSL/TLS (`.crt`) mà chúng ta muốn xuất vào tệp tin PKCS12.

5. `-inkey tech.training.vietnix.tech.key`: Đây là đường dẫn của tệp tin khóa riêng (`.key`) tương ứng với chứng chỉ trên, cũng sẽ được xuất vào tệp tin PKCS12.

6. `-out tech.training.vietnix.tech.pfx`: Đây là tên tệp tin PKCS12 sẽ được tạo ra, chứa cả chứng chỉ và khóa riêng.

Lệnh này sẽ tạo ra file PFX có tên `tech.training.vietnix.tech.pfx` từ file CRT và Private Key.

   
## Domain

### 1. Domain là gì ?

Domain(hay tên miền) là địa chỉ độc nhất của một website trên `Internet`, hoạt động giống như một `Ngôi nhà ảo` chứa đựng toàn bộ nội dung và thông tin của trang web. Thay vì phải ghi nhớ dãy số phức tạp của địa chỉ IP, người dùng có thể dế dàng truy cập website bằng cách nhập tên miền vào trình duyệt.

Domain được cấu thành từ:  Protocol + Sub-Domain + Second-Level Domain(SLD) + Top-Level Domain(TLD) + Page-path

Ví dụ các thành phần của Domain:  https://host247.vietnix.vn/webmail

`https://` : Protocol

`host247`  : Sub-Domain

`vietnix`  : Second-Level Domain(SLD) 

`.vn`      : Top-Level Domain(TLD) 

`/webmail` : Page-PATH

`vietnix.vn` : Domain name

Có 2 loại TLD(Top-Level Domain) chính là `.vn` và Quốc tế(`.com` , `.org` , `.net` ,...) 

Bạn có thể tạo nhiều Sub-Domain để tổ chức Website một cách hiệu quả.

Để domain hoạt động bạn cần [đăng ký tên miền](https://vietnix.vn/dang-ky-ten-mien/) với nhà cung cấp dịch vụ Domain và kết nối nó với Hosting thông qua hệ thống DNS(Domain Name System)

### 2. Các trạng thái phổ biến của một Domain:

- Register (dã đăng ký): Domain đã được đăng ký và thuộc về chủ sở hữu.

- Available (Còn trống): Doamin chưa được đăng ký và có thể được đăng ký.

- Expired (Đã hết hạn): Domain đã hết hạn và cần được gia hạn để tránh bị mất.

- Pending Delete (Chờ xóa): Domain đang trong quá trình bị xóa sau khi hết hạn.

### 4. Subdomain là gì?

Sub-Domain là thành phần của Domain chính, được sử dụng để tổ chức và phân chia nội dung của một trang Website. Ví dụ: `host247.vietnix.vn` là Sub-Domain của `vietnix.vn`


### 5. Virtual Hosts là gì?

Virtual Host là một phương thức lưu trữ cho phép lưu nhiều tên miền khác nhau trên cùng một máy chủ Server. Virtual Hosts có thể được xem như một giải pháp cho phép bạn nhúng rất nhiều tên miền trên một địa chỉ IP của một Server duy nhất. 

Tùy vào cách cài đặt, Server sẽ tự hiểu tên miền nào đang hoạt động bên trong vị trí lưu trứ của Server.

Virtual Host là một giải pháp khá hiệu quả và tiết kiệm chi phí hơn khi sử dụng nhiều tên miền chỉ trên một địa chỉ IP.

- Người dùng có thể dễ dàng truy cập vào bất kỳ một thư mục lưu trữ Code của các trang web khác nhau mà không cần copy code vào thư mục htdocs trong giao diện  XAMMP.

- Trong quá trình thiết lập ban đầu, nếu bạn phân vùng lưu trứ code ở một Folder code  nhất định thì khi cài đặt lại HĐH Windows, bạn không cần sao lưu đồng bộ lại dữ trong Folder code rất tiện lợi.


## Mail Server

### 1. Tìm hiểu MX Record

**Định nghĩa**: MX record là một loại bản ghi DNS (Domain Name System) được sử dụng để chỉ định máy chủ email chính thức của một miền (domain) cụ thể. Khi một email được gửi đến một địa chỉ email trong miền, hệ thống sẽ tham khảo bản ghi MX để xác định nơi lưu trữ và chuyển tiếp email.

**Cấu trúc**: Một bản ghi MX bao gồm hai thành phần chính:
   - Ưu tiên (Priority): Một số nguyên dương từ 0 đến 65535 để xác định thứ tự ưu tiên xử lý email. Số thấp hơn có ưu tiên cao hơn.
   - Tên miền (Domain name): Tên miền của máy chủ email, không phải địa chỉ IP trực tiếp.

![](https://vietnix.vn/wp-content/uploads/2022/10/cac-thuat-ngu-thuong-su-dung-trong-mail-server-5.webp)

**Ưu tiên và Failover**: Việc có nhiều bản ghi MX với các mức ưu tiên khác nhau cung cấp khả năng dự phòng(`failover`) cho các máy chủ email. Nếu máy chủ email chính gặp sự cố, hệ thống sẽ tự động chuyển sang máy chủ email dự phòng có ưu tiên tiếp theo.

**Quản lý Mail Delivery**: Khi gửi email đến một địa chỉ email, hệ thống sẽ thực hiện các bước sau:
   - Truy vấn DNS để tìm bản ghi MX của miền.
   - Liên hệ với máy chủ email có ưu tiên cao nhất trong danh sách bản ghi MX.
   - Nếu máy chủ email chính không phản hồi, sẽ thử liên hệ với máy chủ email có ưu tiên tiếp theo.

**Ứng dụng và Lợi ích**:
   - Cho phép dễ dàng thay đổi địa chỉ IP của máy chủ email mà không cần thay đổi bản ghi MX.
   - Hỗ trợ khả năng dự phòng và gia tăng độ tin cậy của dịch vụ email.
   - Giúp các nhà cung cấp dịch vụ email lọc và chống spam hiệu quả hơn.

Hiểu rõ về MX record là rất quan trọng để quản lý và cấu hình email domain một cách chính xác và hiệu quả.

### 2. Tìm hiểu DKIM, SPF, PTR

#### DKIM (DomainKeys Identified Mail):


***Định nghĩa và Mục đích***:

   - `DKIM` (DomainKeys Identified Mail) là một phương pháp xác thực email được thiết kế để ngăn chặn các cuộc tấn công giả mạo email (email spoofing).

   - Mục đích chính của `DKIM` là giúp người nhận email xác định được email đó thực sự được gửi từ tên miền (domain) mà nó tự xác nhận.

***Cách Thức Hoạt Động***:
   
   - Khi một email được gửi, `DKIM` sẽ tạo ra một chữ ký số (digital signature) và đính kèm vào header của email.
   
   - Chữ ký số này được tạo ra bằng cách sử dụng khóa riêng tư (private key) của tên miền gửi email.
   
   - Khi email được nhận, mail server sẽ sử dụng khóa công khai (public key) của tên miền để xác thực chữ ký số trong email.
   
   - Nếu chữ ký số hợp lệ, email sẽ được coi là đáng tin cậy và không bị giả mạo.

 ***Lợi Ích của DKIM***:
   
   - Ngăn chặn tấn công giả mạo email (email spoofing) bằng cách xác minh domain của người gửi.
   
   - Tăng độ tin cậy và uy tín của email, giúp tránh bị đánh dấu là spam.
   
   - Hỗ trợ các nhà cung cấp dịch vụ email lọc và chống spam hiệu quả hơn.
   
   - Giúp người nhận email có thể xác định email đáng tin cậy và chính xác.

***Cấu Hình DKIM***:

   - Để cài đặt `DKIM`, quản trị viên cần tạo một cặp khóa công khai/riêng tư (public/private key) cho tên miền.
   
   - Khóa công khai sẽ được thêm vào bản ghi DNS của tên miền dưới dạng bản ghi TXT.
   
   - Khóa riêng tư sẽ được sử dụng để ký các email được gửi từ tên miền đó.

#### SPF (Sender Policy Framework):
   
Bản ghi `SPF` được sử dụng chủ yếu để quản lý và kiểm soát luồng email đi từ nội bộ ra bên ngoài thông qua tên miền của tổ chức.

Cụ thể:

1. Nội bộ tổ chức: Bằng cách liệt kê những máy chủ email được phép gửi từ tên miền công ty (ví dụ example.com) trong bản ghi SPF, tổ chức có thể xác định rõ những nguồn email nội bộ được phép sử dụng tên miền này.

2. Bên ngoài tổ chức: Khi email được gửi từ tên miền "example.com" đến bên ngoài, các hệ thống email nhận sẽ kiểm tra bản ghi SPF. Nếu nguồn email không nằm trong danh sách được phép, thì email có thể bị đánh dấu là spam hoặc bị từ chối.

Như vậy, SPF giúp tổ chức kiểm soát chặt chẽ việc sử dụng tên miền công ty trong email, ngăn ngừa các hoạt động giả mạo hoặc lạm dụng tên miền để gửi thư rác từ bên ngoài.

Điều này rất quan trọng để bảo vệ uy tín và tránh email công ty bị nhận nhầm là spam.

#### PTR Record (Pointer Record):
   
   - PTR record được sử dụng để ánh xạ địa chỉ IP thành tên miền.
   
   - Khi một email được gửi đến, mail server sẽ kiểm tra PTR record để xác định tên miền tương ứng với địa chỉ IP của máy chủ gửi email.
   
   - PTR record giúp xác thực danh tính của người gửi email và chống lại các cuộc tấn công spoofing.


## DNS

### 1. DNS là gì ?

> DNS (Domain Name System):

   - DNS là một hệ thống phân cấp dùng để ánh xạ tên miền (domain name) sang địa chỉ IP.

   - Nó giúp người dùng truy cập website bằng tên miền dễ nhớ thay vì phải sử dụng địa chỉ IP khó nhớ. Ví dụ: `265.15.75.210` sẽ khó nhớ hơn `vietnix.com`
   - 
### 2. Các loại recored DNS


> Các loại record DNS:

   - **A record**: Ánh xạ tên miền sang địa chỉ IPv4.

      `www.mywebsite.com. A 192.168.1.100`

      + Giả sử bạn có một wwebsite cá nhân `www.example.com` và website này được lưu trữ trên một máy chủ web có địa chỉ `192.168.1.100`

   - **AAAA record**: Ánh xạ tên miền sang địa chỉ IPv6.
      
      `www.mywebsite.com. AAAA 2001:0db8:85a3:0000:0000:8a2e:0370:7334`

      + Giả sử bạn có một trang website được lưu trữ trên một máy chủ web có địa chỉ IPV6 là như trên.
      
   - **CNAME record**: Tạo bí danh (alias) cho một tên miền.

       `example.com. CNAME www.example.com.`
       
       + Giả sử bạn có một website chính `www.example.com` và muốn tạo một bí danh(alias) `example.com` để người dùng có thể truy cập web site bằng cả 2 tên miền.
        
   - **MX record**: Chỉ định mail server nào sẽ nhận email gửi đến domain.

     ```
     example.com. MX 10 mail.example.com.
     mail.example.com. A 192.168.1.100
     ```
     + Ví dụ, giả sử bạn có một tên miền `example.com` và bạn muốn **email** gửi đến `example.com` được chuyển đến **máy chủ email** có địa chỉ IP `192.168.1.100`.

   - **NS record**: Chỉ định server tên miền nào quản lý một domain.

      ```
      example.com. NS ns1.example.com.
      example.com. NS ns2.example.com.
      ```

      + Ví dụ, giả sử bạn có một tên miền `example.com` và bạn muốn chỉ định rằng tên miền này được quản lý bởi hai máy chủ tên miền: `ns1.example.com` và `ns2.example.com`.

   - **PTR record**: Ánh xạ địa chỉ IP sang tên miền.
       
       ```
       100.1.168.192.in-addr.arpa. PTR mail.example.com.
       ```

       + Ví dụ, giả sử bạn có một địa chỉ IP `192.168.1.100` và bạn muốn xác định tên miền tương ứng với địa chỉ IP này. Trong trường hợp này, bạn sẽ cần tạo một bản ghi PTR như sau:

### 3. Nguyên tắc làm việc của DNS


   - Khi người dùng truy cập một website bằng tên miền, trình duyệt sẽ gửi yêu cầu đến DNS server.
   
   - DNS server sẽ tra cứu các `record DNS` để tìm ra địa chỉ IP tương ứng với tên miền.
   
   - Trình duyệt sẽ sử dụng địa chỉ IP này để thiết lập kết nối với web server.

### 4. Cách phân giải địa chỉ DNS

   - Trình duyệt sẽ kiểm tra `bộ nhớ cache DNS cục bộ` trước. Đây là bộ nhớ lưu trữ các bản ghi mà trình duyệt đã phân giải trước đó.
   
   - Nếu không tìm thấy, trình duyệt sẽ gửi yêu cầu đến DNS server cấp cao hơn (như DNS server của ISP).
   
   - Các DNS server sẽ lần lượt tra cứu các `record DNS` để tìm ra địa chỉ IP cuối cùng.
   
   - Kết quả được trả về cho trình duyệt để thiết lập kết nối.


### Nguồn: [Vietnix](https://vietnix.vn/category/kien-thuc-dich-vu/), [Wikipedia](https://vi.wikipedia.org/wiki/Internet_Protocol), .v.v.... 




### Tác giả: *Quang Huy* 
