THIẾT LẬP VÀ CẤU HÌNH HONEYDRIVE

1.1.	Mô tả
HoneyDrive là môi trường đã được cài đặt sẵn một số Honeypot để thu hút tấn công của tin tặc, giúp người quản trị xây dựng môi trường thử nghiệm. Bản thân HoneyDrive được tích hợp một số công cụ sau:
-	Kippo SSH honeypot
-	Dionaea and Amun malware honeypots
-	Honeyd low-interaction honeypot
-	Glastopf web honeypot and Wordpot
-	Conpot SCADA/ICS honeypot
-	Thug and PhoneyC honeyclients
-	Kippo-Graph, Honeyd-Viz, DionaeaFR, an ELK stack
Trong bài thực hành này hướng dẫn sinh viên sử dụng Kippo SSH Honeypot.
1.2.	Chuẩn bị
	01 máy ảo hệ điều hành Kali linux
	01 máy ảo hệ điều hành HoneyDrive.
	Trình duyệt trên máy vật lý

1.3.	Mô hình cài đặt
<img width="872" height="371" alt="image" src="https://github.com/user-attachments/assets/e5e72313-b4a6-4202-83c6-e1ce70389ae8" />
1.4.	Các bước cài đặt
-	Download phần mềm: https://sourceforge.net/projects/honeydrive/
-	Tải phần mềm dưới dạng máy ảo đã cài sẵn: HoneyDrive_3_Royal_Jelly.ova
Sử dụng phần mềm máy ảo để bung tệp tin ova này thành máy ảo HoneyDrive.
-	Sử dụng máy Kali linux để thực hiện tấn công vào Honeypot SSH kippo
-	Sử dụng trình duyệt trên máy vật lý truy cập vào Kippo-graph trên máy HoneyDrive để phân tích.
1.5.	Thực hiện
Bước 1. Chạy máy ảo HoneyDrive
Sau khi bung nén máy ảo HoneyDrive, khởi chạy máy ảo thành công có giao diện như sau:
<img width="839" height="636" alt="image" src="https://github.com/user-attachments/assets/ffbcd478-8683-439d-9d9b-4cc03da47fe8" />

Tiếp theo cần xác địch địa chỉ IP của máy:
Chạy terminal trên Desktop và sử dụng lệnh ifconfig để xem:
 <img width="426" height="104" alt="image" src="https://github.com/user-attachments/assets/aed746a3-409b-4fb7-9164-2b8dddab73fc" />

 
Bước 2. Chạy chương trình Honeypot kippo
<img width="436" height="87" alt="image" src="https://github.com/user-attachments/assets/481d12f6-fa2b-47df-9928-88fb84f93ea5" />

Bước 3. Quản lý Honeypot Kippo
Trên máy vật lý sử dụng trình duyệt web truy cập vào máy ảo HoneyDrive theo địa chỉ đã xem ở trên và theo đường dẫn sau:
http://192.168.211.151/kippo-graph/
<img width="626" height="335" alt="image" src="https://github.com/user-attachments/assets/7ab7579a-4f8f-4686-ae4e-ebaaed0d8100" />

Bước 4: Kịch bản tấn công dò quét IP và dịch vụ
-	Sử dụng Nmap trên Kali tấn công thăm dò mạng nội bộ:
<img width="403" height="154" alt="image" src="https://github.com/user-attachments/assets/203760da-04e5-4299-8a7c-1722832a7d04" />

 
Phát hiện một số máy tính đang chạy với IP.
-	Thực hiện dò quét dịch vụ và hệ điều hành trên máy 192.168.211.151
<img width="853" height="325" alt="image" src="https://github.com/user-attachments/assets/d1c1ab83-50d4-426b-9ee9-f07ca102d6c1" />


Kết quả phát hiện dịch vụ SSH và web đang chạy trên cổng 22, 80. Hệ điều hành máy đích là Linux => khả năng đây là máy chủ web.
Kẻ tấn công thực hiện các bước mà không phát hiện ra họ đang tấn công vào dịch vụ của Honeypot.
Bước 5. Kịch bản tấn công mật khẩu dịch vụ SSH
Sử dụng Hydra trên Linux tấn công từ điển vào mật dịch vụ SSH
<img width="475" height="123" alt="image" src="https://github.com/user-attachments/assets/7b2def81-d34d-46ba-ac94-e62d8db38e27" />


Kết quả thành công, thu được mật khẩu của tài khoản root.
Bước 6. Truy cập vào máy chủ thông qua dịch vụ SSH
Với tài khoản và mật khẩu đã có, kẻ tấn công thực hiện lệnh kết nối tới máy
chủ:
<img width="743" height="654" alt="image" src="https://github.com/user-attachments/assets/d15fabd6-53e5-4324-a938-2771dbc05ba6" />

Truy cập thành công.
 
Bước 7. Thực hiện một số lệnh trên máy chủ
<img width="392" height="254" alt="image" src="https://github.com/user-attachments/assets/093b92ff-9649-44f9-ab60-a10e51cc8354" />
<img width="213" height="61" alt="image" src="https://github.com/user-attachments/assets/e36d3971-b1c0-4840-ad7e-fdd3e7b2d24a" />
<img width="215" height="41" alt="image" src="https://github.com/user-attachments/assets/ba38aabc-8966-428b-93cb-62ff39996c41" />



Bước 8. Phân tích hành vi
Tại trình duyệt Kippo đã bật trong bước 3. Refresh lại trình duyệt thì kết quả như sau:
<img width="617" height="301" alt="image" src="https://github.com/user-attachments/assets/b23ea1c1-2768-427f-bb9a-5bdfcb1884b0" />


Giao diện này cho biết mật khẩu và số lượng tin tặc đã sử dụng.
 
 <img width="613" height="195" alt="image" src="https://github.com/user-attachments/assets/dd01ae73-e6c1-4fdb-8d16-4966ddf5da03" />

Giao diện này cho biết tài khoản và số lần đăng nhập.
<img width="976" height="330" alt="image" src="https://github.com/user-attachments/assets/551b3935-54f1-4837-8f13-4d2b7a2137ba" />


Giao diện này cho biết tài khoản được đăng nhập bởi mật khẩu tương ứng.
<img width="975" height="509" alt="image" src="https://github.com/user-attachments/assets/065e4812-47f8-44b4-a3c2-110c72a2c18b" />

Giao diện này cho biết số lần đăng nhập đúng và sai.
 
 <img width="970" height="500" alt="image" src="https://github.com/user-attachments/assets/5def721b-20d9-4577-b79d-880e990d2c45" />

Giao diện này cho biết IP của tin tặc đã sử dụng để xâm nhập vào máy chủ Honeypot.
Chuyển sang Tab Kippo-Input để phân tích một số lệnh tin tặc đã sử dụng
<img width="621" height="169" alt="image" src="https://github.com/user-attachments/assets/77873749-0ff1-44e4-80a7-0b9b5a087ca8" />

Kết luận:
Với HoneyDrive người quản trị có thể sử dụng để thực hiện một số Honeypot để thu hút tấn công của tin tặc. Từ đó biết được cách thức tấn công, dịch vụ bị tấn công. Vì vậy mà người quản trị có thể đưa ra các giải pháp ngăn chặn cho hệ thống thực.


