# Class Project
>## Description: 
>I was working on a project for my C programming class and I broke my VM when trying to compile my code! My project is due at 11:59. Can you please help me get my VM up and running again?<br>
>VM Password: 1_w1ll_n07_br34k_7h15
>
><br>Download file: https://drive.google.com/drive/folders/1gE4Idj6DjhJ3AX64tOL3Tp31k8gurj94?usp=sharing
><br>Author: amanthanvi<br>
>Solves: 29/553

# Solver:
Đề bài cho các file máy ảo <br>
![image](https://user-images.githubusercontent.com/75996090/157261256-ce499ba2-9f3a-4095-a4cd-61b9305f61a8.png)
<br>Import vào VMware và đăng nhập với mật khẩu đề cho. Tuy nhiên bạn có thể thấy sau khi đăng nhập khoảng 10s thôi là máy bắt đầu đơ. 
<br>Lý do là vì có một fork bomb trong autostart. Nó là một kiểu tấn công từ chối dịch vụ (DoS) trong đó fork system call được sử dụng một cách đệ quy cho đến khi tất cả tài nguyên hệ thống thực thi một lệnh khiến hệ thống cuối cùng trở nên quá tải và tê liệt, không thể phản hồi bất kỳ đầu vào nào.
<br>Vì vậy ý tưởng ở đây là phải khởi động trực tiếp tới root bằng cách chỉnh sửa grub command line để khám phá hệ thống tệp ([tham khảo](https://frameboxxindore.com/android/how-do-i-boot-ubuntu-as-root.html))
<br>Tuy nhiên k hiểu vì một lý do gì đó mà mình ko làm được nên mình làm hơi khác đi một chút
#### Tiến hành khởi động lại máy ảo. Trong khi BOOT đang load thì nhanh chóng ấn Shift. Màn hình sẽ hiển thị menu GNU GRUB
<br>![image](https://user-images.githubusercontent.com/75996090/157273651-96ebe5f9-68b3-4108-a6db-0349996391eb.png)
#### Ấn `c` để mở grub command line
![image](https://user-images.githubusercontent.com/75996090/157277179-c17e69f3-ab39-411f-a8f9-778a91d8650e.png)
#### Giờ chỉ việc cd tới các phân vùng và các tệp để tìm flag thôi
![image](https://user-images.githubusercontent.com/75996090/157277505-fe6e5c1b-c3db-4e25-9771-e238e9e2d8e8.png)
#### Flag được để trong file `(hd0,msdos5)/home/aman_esc/Documents/admin_notes` và trong cùng thư mục thì còn có file `fork_bomb.bash`, nguyên nhân khiến máy tính bị đơ
![FLAG ne](https://user-images.githubusercontent.com/75996090/157278339-40c9c6c0-4a8f-4632-bff4-3706039cbbbc.png)

### Flag: UMDCTF{f0rk_b0mb5_4r3_4_b4d_71m3}
