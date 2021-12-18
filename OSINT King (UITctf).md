# Challenge: OSINT King

### Description: 
Will Barrow is an Open-Source Intelligence Analyst, so he keeps his personal information private at all times. However, by mistake, he once revealed his personal information. Try searching and see if you can find any of his secrets, knowing that he is using a social question-and-answer platform and i think it is not the only one since he is an influencer.
### Difficulty:
Hard

# Solver:
## Phase 1:
#### Đầu tiên, tìm mạng xã hội được nhắc đến ở đề bài. Copy nguyên đoạn `social question-and-answer platform`, tìm được mxh này là `Quora`<br>
![image](https://user-images.githubusercontent.com/75996090/146077431-a3eeeb6f-4f77-4807-adc8-96e018503a3e.png)
 <br>
#### Tiếp tục sử dụng search engine là Quora và một chút dorking `"Will Barrow"` + sort by profiles <br>
![image](https://user-images.githubusercontent.com/75996090/146077573-9e29cac4-0407-4161-bfae-bcd235332ed9.png)
#### Giao diện tường nhà Will Barrow:
![image](https://user-images.githubusercontent.com/75996090/146627708-16d4dc0e-6f83-467f-9258-60eea1b62ed7.png)
#### Sau khi tốn thời gian vào những cái linh tinh thì mình thấy một thứ thú vị trong phần `Edits` (logs)
![image](https://user-images.githubusercontent.com/75996090/146077712-6e530804-48cf-4477-b0fb-01a35380360c.png)

- Lý do có phần này là vì Will Barrow đã vô tình đăng một nội dung gì đó và khi nhận ra bị lộ thông tin thì anh ta đã xóa nó đi, tuy nhiên trước khi xóa thì anh ta đã từng sửa nó nên Quora có lưu lại thông tin này => Đây có thể là điều mà Will Barrow không biết
#### Khi ấn vào `Post deleted` và nhìn lên thanh url, mình thấy nội dung bài post đã được Quora lưu lại
![image](https://user-images.githubusercontent.com/75996090/146075833-7c5c1aaa-3884-4182-8769-dbb50f2725f1.png)
#### Mình nhận ra đây là link ảnh imgur, sửa lại một chút, replace("-", "/") để lấy link gốc: https://imgur.com/a/KkR6760
![image](https://user-images.githubusercontent.com/75996090/146627747-fecc5c28-35e2-4cc3-a7bb-015391a71a94.png)
- Ảnh cơ bản là không có gì, chỉ là việc anh ta chia sẻ tool sherlock với mọi người thôi.
#### Tuy nhiên mình nhận ra rằng anh ta có sử dụng `Gitlab` nữa.
## Phase 2:
#### Tiếp tục dùng gitlab làm công cụ tìm kiếm và sau một thời gian tìm kiếm, mình thấy anh ta với cái tên viết tắt `WBarrow` giống mô tả trong Quora
![image](https://user-images.githubusercontent.com/75996090/146077264-131eac67-91c4-4639-9466-a5fb241f4563.png)
#### Overview
![image](https://user-images.githubusercontent.com/75996090/146627788-6128b3f5-bb2e-4a13-bc5b-3f60a11eeed2.png)
#### Có 2 repo, sau khi kiểm tra không có gì thú vị thì mình quyết định sử dụng kỹ thuật để tìm email từ gitlab. 
- Với kinh nghiệm OSINT của mình thì nếu từ các commit mới không lấy được email thì phải thử với các commit siêu cũ, vì có thể lúc đó người ta chưa bật cơ chế bảo vệ email. 
#### Do commit đầu tiên trong gitlab không xem được dữ liệu nên mình thử với commit thứ 2 từ dưới lên, thêm `.patch` vào cuối https://gitlab.com/9it14b-wi11b4rr0w/hello-world/-/commit/c9292575a394724947cc6288b61b669442396758.patch 
![image](https://user-images.githubusercontent.com/75996090/146079604-d9dd4634-2202-4667-9ae7-bf597b086282.png)
#### Tuyệt vời!!! Tìm được email của Will Barrow: `pr0t0nm4i1-wi11b4rr0w@protonmail.com`
#### Sử dụng [holehe](https://github.com/megadose/holehe) hoặc [Epieos](https://tools.epieos.com/email.php)(vẫn là holehe) để tìm các mxh được đăng kí cùng một email, mình thấy rằng Will Barrow đang sử dụng một xã hội khác là `Ello`
![image](https://user-images.githubusercontent.com/75996090/146080614-1511021a-0a13-4c2d-80a2-88dadc23dbdb.png)
## Phase 3:
#### Sau khi tìm Will Barrow trên Ello không thành công, mình quay lại Quora và tổng hợp lại được một số thứ thú vị sau:
1. Username gitlab: `9it14b-wi11b4rr0w`
2. Username protonmai: `pr0t0nm4i1-wi11b4rr0w`
3. ![image](https://user-images.githubusercontent.com/75996090/146082143-fa1c6aea-6600-432a-8215-2587ef8cc2d3.png)
4. ![image](https://user-images.githubusercontent.com/75996090/146082174-1b84c998-a3a0-4db1-94b5-96487242f25e.png)
- Số 3 và số 4 là các tip được chia sẻ trên Quora của Will Barrow
### ==> 4 điều trên cho thấy thói quen của Will Barrow khi đặt username là:
```python
leet('social media/network' + "-" + "willbarrow")
#j4f x)
```
#### Từ đó dễ dàng đoán được tên Ello username là: `3110-wi11b4rr0w`
![image](https://user-images.githubusercontent.com/75996090/146628035-158285a7-3cfd-448a-9217-7949496d39a3.png)

#### Bài post đáng được quan tâm 
![image](https://user-images.githubusercontent.com/75996090/146084102-e9847392-9972-4d68-ae90-a84d049a31fb.png)
### Vậy là chúng ta đã đi khá xa rồi và có vẻ đây là nơi có flag. Nhưng flag ở đâu?
#### Sau khi để ý kĩ ảnh bìa thì mình nhận ra đây là ảnh đã được đăng trên Quora nhưng bị thiếu một chút phần dưới, khá đáng nghi 
- Quora
<br> ![image](https://user-images.githubusercontent.com/75996090/146085065-8c77fb7c-82b0-42f5-8cb9-44398be5c36b.png)
- Ello
<br>![image](https://user-images.githubusercontent.com/75996090/146084958-3350337f-72c9-4067-ba77-76703779f47d.png)
#### Mình quyết định xem đầy đủ ảnh bìa
![image](https://user-images.githubusercontent.com/75996090/146133604-d0da5c8d-a966-4551-91b2-8ebe74ea2398.png)
#### Và đây là link ảnh: https://assets3.ello.co/uploads/user/cover_image/5216858/ello-xhdpi-2018abde.jpg
![image](https://user-images.githubusercontent.com/75996090/146133893-31da1018-7af7-42fa-8a41-cadca9e56768.png)
#### Lụm tiền!!!!
### Flag: Wanna.One{Do_you_smile_when_you_find_this_flag?Merry_Xmas}

## Quảng cáo: Mình cũng có một số challenge OSINT, bạn nào cảm thấy hứng thú với OSINT thì có thể tham khảo ở đây nhé: https://wargame.whitehat.vn/
