### DETECTIVE

![image](https://user-images.githubusercontent.com/75996090/208670705-35ffb2ec-d235-4025-b7f6-58f3bac803c5.png)

### Unintended Solution

Trong file bài `Another` có chứa flag của bài này có lẽ là do tác giả chưa xóa file build bài này khi thu thập dữ liệu cho bài Another

![image](https://user-images.githubusercontent.com/75996090/208703586-05717a6b-9b4f-4ec6-a172-379d4133b132.png)

### Intended Solution

Mô tả bài nói là Alan Fresco chỉ reply email có tiêu đề `Applying for detective role` nên mình có làm theo và nhận đc một email phản hồi tự động

![image](https://user-images.githubusercontent.com/75996090/208674484-a5699cd7-3f5f-409d-b373-4ad2991ca030.png)

List các câu hỏi cần trả lời

![image](https://user-images.githubusercontent.com/75996090/208674696-51c815b5-7a75-4539-acda-8dc2c431cafa.png)


#### [1]. What is my full name?

Câu hỏi này thì ko phải nghĩ, tên email to đùng kia rồi

> Answer 1: AlanFresco

Tiếp theo để khai thác thêm thông tin, mình đi osint email **tosang3123003@gmail.com** bằng `ghunt` và `holehe`

![image](https://user-images.githubusercontent.com/75996090/208697547-4be80ff5-baa8-41d5-8118-d9f177c0e2a5.png)

Dựa vào ghunt, ta có thể xem google map contribution và Google Calendar của chủ email.

Từ gg map contribute mình có thấy một review của chủ email trong đó có chứa sđt là `+12025550196`, tuy nhiên lúc mình viết wu này thì nó ko còn nữa, có thể là do ai đó đã report nên comment bị xóa rồi :3 

> Answer 10: `+12025550196`

Trong gg calender của chủ email có thông tin về sự kiện được đặt lịch là deadline để apply cho công việc. Chuyển thời gian sang timestamp được `1671618600`

![image](https://user-images.githubusercontent.com/75996090/208704701-2af56bf1-d5eb-4abc-821d-5888810a09c3.png)


> Answer 6: `1671618600`

![image](https://user-images.githubusercontent.com/75996090/208699243-7ff7f28a-6349-4bf7-8b23-10b806028b1b.png)

Dựa vào `holehe`, ta xác định được email này được sử dụng để tạo tài khoản **github** và **flickr**

Có nhiều cách để tìm github từ một email và [blog này](https://dev.to/martiliones/how-i-got-linus-torvalds-in-my-contributors-on-github-3k4g) sử dụng một thủ thuật khá hay, nhờ đó mình tìm đc github của Alan Fresco: https://github.com/alang1thup 

Thông tin từ phần giới thiệu và các repositories cho thấy dự án mà anh ta đang phát triển là `TheClumptimester`

> Answer 7: `TheClumptimester`

Ban đầu mình nghĩ phần source của TheClumptimester sẽ cho đáp án về ngôn ngữ được sử dụng để trả lời cho câu hỏi 3 nhưng không, lục tung github lên vẫn ko thấy một dòng code nào -_-

Sau một hồi mò mẫm thì mình chợt nhớ ra github còn có một cái gọi là gist dùng để lưu mấy đoạn mã ngắn và sau khi [vào đây](https://gist.github.com/alang1thup) thì đúng là có thông tin về program đầu tiên của A.F, ngôn ngữ đc sử dụng là **Hashkell**

> Answer 3: `Hashkell`

Có vẻ là tìm đc hết thông tin từ Github rồi nên mình chuyển sang OSINT Flickr

Có email trong tay nên việc tìm username Flickr cũng khá đơn giản

![image](https://user-images.githubusercontent.com/75996090/208708428-52cae030-de70-4819-8ba3-cd37d9334b32.png)

> Answer 8: `A.Fr35c0`

Ảnh trong bộ sưu tập cùng caption trong ảnh cho thấy lửng mật (Ratel) là con vật yêu thích của anh ta

> Answer 2: `Ratel`

Do không tìm thấy thông tin gì cho các câu hỏi còn lại nên mình tiếp tục chuyển sang tìm thông tin trên các nền tảng khác và tìm thấy [Facebook](https://www.facebook.com/profile.php?id=100087791405260) của anh ta, ngoài ra còn có liên kết tới [Linkedin](https://www.linkedin.com/in/alan-fresco-976377258/)

Kết hợp thông tin ngày sinh và năm sinh từ 2 nền tảng, ta đc câu trả lời cho câu hỏi 4

![image](https://user-images.githubusercontent.com/75996090/208713923-9287dacc-65c8-47ba-9f0c-e4d0dc09f456.png)

![image](https://user-images.githubusercontent.com/75996090/208713948-c958a3f8-f230-451f-b18e-0b07c8eeb9db.png)

> Answer 4: `06061982`

Trong phần **Experience** trên Linkedin cho ta thông tin về nơi làm việc của anh ta trong năm 2018, trong thời gian đó thì anh ta vẫn đang làm việc tại `GardaWorld`

![image](https://user-images.githubusercontent.com/75996090/208714283-ef9e9445-03be-4fc2-bdfe-866b0ad5eb08.png)

> Answer 9: `GardaWorld`

#### [5]. The coordinates where the photo was taken in Album "Neighborhood"

Thông tin về tọa độ cho câu trả lời này có thể được tìm thấy trên Flickr tuy nhiên do trong lúc giải, mình tìm đc Facebook trước Flickr nên đã tốn thời gian để OSINT địa điểm này

Đây là bức ảnh được đăng trong Album "Neighborhood" trên Facebook

![image](https://user-images.githubusercontent.com/75996090/208715267-4120d5b0-a5ad-4399-8937-db2aed1c870d.png)

Khi focus vào con tàu trong ảnh thì mình nhận ra đây là một tàu chiến

![image](https://user-images.githubusercontent.com/75996090/208715602-123215ed-100c-42b6-88ae-c0ceab485c5f.png)

Vì vậy mình đoán nơi bức ảnh này được chụp có lẽ gần một khu căn cứ hải quân. 

Cộng thêm một số thông tin trên Facebook và Linkedin cho thấy Alan Fresco đang sống ở Washington nên mình đã google các khu căn cứ hải quân ở Washington và may mắn là chỉ có duy nhất 1 cái là **Naval Base Kitsap**

![image](https://user-images.githubusercontent.com/75996090/208716557-c1cd7b21-4907-4111-a7fc-fe92b7535368.png)

Để ý bức ảnh có thể thấy bức ảnh được chụp trên một con đường dọc bờ biển mà trong google maps thì chỉ có một đoạn đường trông giống ảnh mà được phép "thả người" để xem chế độ xem phố thôi nên mình thả luôn vào đó

![image](https://user-images.githubusercontent.com/75996090/208717637-d2e6cc64-aad0-49de-b876-68a132ee6b3f.png)

Sau một chút điều chỉnh vị trí đứng thì mình tìm đc tọa độ y hệt ảnh

![image](https://user-images.githubusercontent.com/75996090/208718064-f83396a6-5357-4d84-a820-81cfe744067c.png)

> Answer 5: `47.55,-122.66`

![image](https://user-images.githubusercontent.com/75996090/208718378-5f7171c5-3ba0-48bf-b7b3-22769ac42437.png)

#### Flag: ISITDTU{I_n3vER_0nc3_r3gR3t73d_d01n9_Tru3_D3t3ct1v3}
