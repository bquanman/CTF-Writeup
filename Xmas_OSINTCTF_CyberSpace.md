# Xmas OSINT CTF Cyber Space
## Description:
#### Chuyện là vừa có một email khẩn cấp vừa được gởi đến cho chúng mình có nội dung như sau:
"Chúng tôi đến từ Trung tâm Tình báo Nam Cực (Antarctica Central Intelligence).
Ngài Santa Claus đã được trình báo mất tích từ 3 ngày trước, và mới hôm qua, Mr. X, thủ lĩnh bang hội The Unknowns đã lên tiếng nhận trách nhiệm cho vụ bắt cóc này. Với nguồn lực hiện tại của ACI, chúng tôi chưa thể tìm ra manh mối nào dẫn đến nơi giam giữ Santa Claus.
Biết được độc giả của Cyber Space là những bậc thầy lão làng trong lĩnh vực OSINT, chúng tôi kêu gọi sự giúp đỡ của các bạn để giải cứu Santa Claus trước đêm Giáng Sinh.
Mọi thông tin có ích dẫn đến nơi ngài Santa đang bị giam giữ đều sẽ được hậu thuẫn xứng đáng.
Chúc các bạn may mắn!<br>
Erica Semira."

## Solver:
#### [Warm-up xíu nhỉ](https://bit.ly/3Ji8OMq)
#### Sau khi lướt qua đề bài thì mình xác định được ngay cái tên cần OSINT là `Erica Semira`. Mình thử tìm kiếm trên google và một số mxh lớn như twitter, facebook, linkedin thì may mắn tìm được người này trên linkedin https://www.linkedin.com/in/erica-semira-365917228/ cùng một chiếc flag lồ lộ ngay bên dưới, chỉ cần đảo ngược lại là được flag đúng
![image](https://user-images.githubusercontent.com/75996090/147370822-90284c3c-a68e-480f-a2e4-3058fd90d42d.png)
### Flag3: CSFLAG3_CM2021{34sy_70_f1nd}

#### Trong phần **Contect info** của người này có chứa liên kết tới reddit của cô ấy.
![image](https://user-images.githubusercontent.com/75996090/147370894-68dbbafb-4dc4-49e8-9058-011c727eadfe.png)
#### Mình nghĩ có một flag trong các bản lưu reddit nhưng chưa tìm đc. Các bạn có thể thử https://web.archive.org hoặc https://archive.ph
#### Reddit không có gì ngoài vài cái link lừa :3. Thứ duy nhất có giá trị là chiếc username, dùng sherlock thì mình thấy cô ấy có sử dụng username này cho Quora nữa.
#### Trên tường nhà là chiếc flag 2 nhưng nội dung trong flag thì mình phải geoguess tiếp.
![image](https://user-images.githubusercontent.com/75996090/147371002-fc9ff6c5-6775-4aee-88f5-59ec9aba8562.png)
#### Do cảm thấy tốn thời gian nên mình không tập trung giải mà sau khi hết giải mình mới thử và tìm được địa điểm này là Palmer Station
![image](https://user-images.githubusercontent.com/75996090/147371020-b23b56e2-e415-4ec2-ad6a-a6240f6f8cdb.png)
### Flag2:  CSFLAG2_CM2021{Palmer_Station}

#### Trên reddit của Erica có một link drive https://drive.google.com/drive/folders/1YZ656AG7qAz7L_xEJ4CK0PT0ZQLPHBfQ. Sau khi ấn vào và tải file xuống, mình thấy trong file chứa rất nhiều ảnh và file chứa ảnh. Vì thế nên mình hơi nản, mình bỏ lại file drive đó và chuyển sang OSINT các thông tin khác của Erica. Đây là sai lầm của mình khi dành quá nhiều thời gian vào việc này tuy nhiên mình vẫn chia sẻ vì có thể có bạn chưa biết.
#### Ấn chuột phải vào một thư mục bất kì, gmail chủ sở hữu sẽ hiện ra 
![image](https://user-images.githubusercontent.com/75996090/147371532-4d61e9f7-0c32-4a85-a27b-230c5dfe85b5.png)
#### Sau đó mình đâm đầu vào OSINT chiếc email này với hàng tá cách khác nhau nhưng không nhận lại được gì. Cho đến khi vài cái flag bị blood thì mình mới tỉnh ngộ :) và quay lại tìm kiếm trong đống ảnh kia vì nó mới có chìa khóa để mở các cánh cổng tiếp theo
#### Đầu tiên mình dùng **tree** để show hết thư mục. Có quá nhiều thư mục và hình ảnh, tuy nhiên hầu như là ảnh jpg, vì vậy mình loại các chuỗi có chứa jpg và lúc này kết quả cho ra ổn hơn nhiều https://pastebin.com/WzqzcKAa
#### Dễ dàng nhìn thấy **Classified documents**, và 2 file txt là đáng nghi. Sau khi kiểm tra 2 file txt đều là lừa thì mình đến thư mục **Classified document**: `06-20-2021/PEQJDRivHKzNp/lZ51DQ2PKkXAn/Classified documents`
#### Ở đây có bức ảnh **g37tptUqyTg4iUQ.jpg** có chứa flag 4, do hơi tối nên mình đã chỉnh độ sáng và độ tương phản một tí cho dễ nhìn
![image](https://user-images.githubusercontent.com/75996090/147398589-6f4243d7-f1c0-4c5e-bc90-84553305cef8.png)
#### Flag RHUAPV4_RB2021{h4S_3me3g1Tcr3} -> rot11: `CSFLAG4_CM2021{s4D_3xp3r1Enc3}`

#### Bên cạnh đó có 3 hình ảnh hồ sơ vụ án liên quan đến băng đảng The Unknowns ở đây chứa nguồn thông tin rất lớn để tìm các flag sau.
## Picture-3.jpg
#### Đầu tiên đi vào hình ảnh **picture-3.jpg**
![picture-3](https://user-images.githubusercontent.com/75996090/147381289-f18236e0-70f5-449b-84df-284f27b64fa2.jpg)
#### Mình thấy 1 username **Cow_Lee**. Dùng sherlock thấy 1 tài khoản reddit https://www.reddit.com/user/Cow_Lee
![image](https://user-images.githubusercontent.com/75996090/147381386-5b18c520-4427-4209-84bb-f9c75f8872de.png)
#### Có 1 email ở đây. Mình dùng https://tools.epieos.com/email.php (Ghunt) để tìm thì thấy [link ggmap](https://www.google.com/maps/contrib/102844024063222071910) của ng này, ở đây có 1 bình luận chứa flag. Tuy nhiên hình như nó đã bị ai đó report nên khi mình viết writeup này thì nó ko còn nữa
### Flag9: CSFLAG9_CM2021{u_c4m3_t0_th3_r1ght_pl4c3}

#### Bên cạnh tên Carl Le có gợi ý **Contact for work** ý muốn ám chỉ mình contact cho họ bằng gmail bên dưới. Gửi email tới `alnewnfweo1ufh@gmail.com` với nội dung bất kì, mình nhận đc email trả lời tự động có chứa 1 link ảnh https://ibb.co/nrPxZsp.
#### Dựa vào một loạt hint ở reddit thì mình biết được đây là một puzzle mang tên **Cicada 3301**(gg để biết thêm về tổ chức bí ẩn này). Google tiếp thì mình thấy [walkthrough này](https://www.boxentriq.com/code-breaking/cicada-3301-first-puzzle-walkthrough), dựa vào đây để chơi thôi.
#### Đầu tiên ném hình ảnh bên trên vô https://aperisolve.fr/ rồi download Outguess file
![image](https://user-images.githubusercontent.com/75996090/147383864-26a6921d-523f-4026-bb57-4313313e8397.png)
#### Nhận được message:
```
Hi. You found the hidden message. To advance to the next stage, there are three prime numbers associated with this image, 3301 is one of them. Find the other twos, multiply them and visit the subreddit r/<product_of_3_prime_number>. You will find the instructions for further steps. Good luck.
```
#### Chúng ta phải tìm 3 số nguyên tố liên quan đến hình ảnh rồi nhân chúng lại để lấy subreddit. 3 số nguyên tố đó chính là chiều dài (641), chiều rộng (643) của ảnh và số 3301. Nhân lại ta được link reddit https://www.reddit.com/r/1360550063/
#### Người điều hành reddit cũng là người đã đăng tất cả reddit là https://www.reddit.com/user/botezgambit2277/
#### Tiếp tục nhận được link imgbb ở đây https://ibb.co/dr71cV7 (thực ra có 2 link nhưng mình đoán do link đầu tiên admin cho thiếu thông tin nên đăng lại). Và lại tiếp tục ném lên aperisolve.fr :) 
#### Trong phần metadata của ảnh có một link https://pastebin.com/yZNuRYTJ, và download Outguess nhận được `Key: ihalmtbuhyxatajqlsnevewzutzidicAOAGQnoglawdwg`
#### Vào link pastebin trước, mình thấy một loạt các tọa độ ở đây và các tọa độ không quá cách xa nhau, vì vậy ý tưởng là nối các tọa độ này trên map có thể nhận được flag. 
![image](https://user-images.githubusercontent.com/75996090/147383957-e3ffa433-8bd1-4878-b653-51197a35c867.png)
#### Tìm kiếm cách import các tọa độ vào gg map rồi làm theo (https://www.youtube.com/watch?v=XRD9a2jlUcY), mình nhận được 2 nửa của flag xịn
![image](https://user-images.githubusercontent.com/75996090/147382111-e1e8364f-31c9-4e01-a02c-994c50019391.png)
### Flag: CSFLAG_CM2021{u_found_me!}

#### Quay lại đọc walkthrough, mình hiểu các đoạn post được botezgambit2277 đăng thực chất là 1 văn bản bị cắt ra và bị mã hóa Vigenere bằng key `ihalmtbuhyxatajqlsnevewzutzidicAOAGQnoglawdwg`.
![image](https://user-images.githubusercontent.com/75996090/147383970-8de00995-34c7-42eb-9e8a-a41f8a1d2ee9.png)
#### Dùng Cryptii giai mã xong mình nhận được key: `THISISTHEKEYFORFLAG`. Tiếp tục decode key `ihalmtbuhyxatajqlsnevewzutzidicAOAGQnoglawdwg` bằng key `THISISTHEKEYFORFLAG`mới nhận được này, mình nhận được message là link pastebin chứa flag xịn thứ 2 https://pastebin.com/tVAJBF97
![image](https://user-images.githubusercontent.com/75996090/147384023-6c112f08-6603-4f89-a311-a6ccec63e5c3.png)
### Flag: CSFLAG_CM2021{D0ubl3_cH3ck3d}

#### Bên cạnh những thứ này, botezgambit2277 còn đăng một link ggsheet nữa và dựa vào link ggsheet này, có một mẹo để tìm ra email chủ sở hữu và mình đã nghĩ ra.
#### Đầu tiên các bạn chọn gắn dấu sao hoặc thêm lối tắt vào drive
![image](https://user-images.githubusercontent.com/75996090/147382376-f9526ced-1ac0-490e-bf0a-1a5f1d8307ec.png)
#### Sau đó vào drive của mình (https://drive.google.com), cái sheet kia sẽ ở ngay trên đầu phần đề xuất, chuột phải để xem email thôi. trxncc3pt1234@gmail.com
- Gần đây thì mình mới biết rằng có công cụ có thể tự động hóa việc tìm email từ sheet là [Ghunt](https://github.com/mxrch/GHunt) và [xeuledoc](https://github.com/Malfrats/xeuledoc). Tuy nhiên thì mình thấy làm tay vẫn nhanh hơn :D <br>
![image](https://user-images.githubusercontent.com/75996090/147382452-abdd72ab-3fdb-4c0f-8603-ca562a6c3e09.png)
#### Tiếp tục dùng Ghunt, mình thấy ở ggmap của ng này có 1 flag nhưng sau khi submit xong mình mới nhận ra sai format, hóa ra là flag của giải cũ. Tưởng cái email này không cần thiết và không cần phải đào sâu như vậy nên mình đã bỏ đi. Cho đến khi admin hint trên page thì mình mới nhớ ra là chưa gửi email cho địa chỉ đó, đôi khi dễ quá lại không nghĩ đến :v.
![image](https://user-images.githubusercontent.com/75996090/147403186-3eb25c46-d7f2-41e1-93df-55d38f534a9a.png)
#### Email auto-reply có chứa flag: CSFLAG10_CM2021{sk1ll3d_pl4y3r}

## Picture-2.jpg
#### Ảnh 2 có chứa link wordpress: https://thetruthnews423666022.wordpress.com/
#### Sau khi lục lọi một lúc mình thấy flag ở bài viết này: https://thetruthnews423666022.wordpress.com/2021/12/15/about-us/
![image](https://user-images.githubusercontent.com/75996090/147382742-fdf5350c-c4db-4804-a666-13f4874d8ffb.png)
#### Decode hex -> decode base64, flag 7 xuất hiện
### Flag7: CSFLAG7_CM2021{w3LL_m3t_StR4ng3rz}

![image](https://user-images.githubusercontent.com/75996090/147403122-330b5cee-da8e-40da-8345-aa34659b0fb8.png)
#### Nếu các bạn để ý và ấn vào phần tác giả của các bài viết là `K ED`, username tác giả sẽ hiện ra trên url (https://thetruthnews423666022.wordpress.com/author/karendouche1412/)
![image](https://user-images.githubusercontent.com/75996090/147403133-6a171fe6-90e1-4709-957c-ca5eb2ed9e9e.png)
#### Dùng `sherlock` với username `karendouche1412`, nhận được facebook người này: https://www.facebook.com/karendouche1412/
#### Một số thông tin quan trọng trên facebook nói về password, the first Game of War player... sẽ có ích về sau.
#### Từ tên facebook **Karen Douche**, tìm đc linkedin
![image](https://user-images.githubusercontent.com/75996090/147403708-c3855ef5-7bab-43a1-8ab1-0f3ea4d3f2f3.png)
#### Wordpress của người này: https://karenskitchen101286359.wordpress.com/
#### Lục lọi một lúc, sau khi ấn vào phần author `K ED` như bên trên hoặc admin đã làm nó dễ dàng hơn một chút bằng cách nhấn vào đây
![image](https://user-images.githubusercontent.com/75996090/147404320-d89c00ab-3ead-4012-9089-69628e49653b.png)
#### Mình thấy một [hidden protected blog](https://karenskitchen101286359.wordpress.com/2021/12/11/reality-is-often-disappointing/)
![image](https://user-images.githubusercontent.com/75996090/147403907-c926e307-6c9d-4f4f-85d4-f9f7769d011e.png)
#### Quay lại facebook đọc các bài post, mình hiểu rằng password là tên của `first Game of War player`
![image](https://user-images.githubusercontent.com/75996090/147403967-74b57ef4-9c76-4c61-85a5-686a19809471.png)
![image](https://user-images.githubusercontent.com/75996090/147403982-221afb45-a1df-4d47-836a-386b7708a274.png)
#### Lúc đầu ý tưởng của mình là tải game `Game of War` trên CHPlay về rồi tìm nhân vật có tên Karen Douche sau đó tìm danh sách bạn của người đó nhưng nohope. Cho đến khi admin tung hint số 4 
![image](https://user-images.githubusercontent.com/75996090/147404481-17063dd0-6c62-4041-9101-3bfe7e97b347.png)
#### Google và mình tìm đc tên người này là `TheLegend27`. Nhập mật khẩu và nhận được một nửa flag
![image](https://user-images.githubusercontent.com/75996090/147404544-8e415d1c-30f0-47f6-ac09-5a626731af2d.png)
#### Bên dưới còn có một comment để từ đó tìm pastebin
![image](https://user-images.githubusercontent.com/75996090/147404563-01ef96ce-70eb-4447-94ae-e783fae9e707.png)
![image](https://user-images.githubusercontent.com/75996090/147404636-38c27d31-bb19-4158-9b50-4ac5dccfb5c1.png)
#### Nội dung của Paste thứ 3:
![image](https://user-images.githubusercontent.com/75996090/147404955-d7db3495-d39e-41a8-98db-a24b9d6bd348.png)
#### Vậy là wordpress có một hidden site đường dẫn là `/15_4`. Sau rất lâu mình mới hiểu rằng 15 và 4 là các ô chữ trong [crossword puzzle blog](https://karenskitchen101286359.wordpress.com/2021/12/11/i-like-a-crossword-for-my-customers/) 
![image](https://user-images.githubusercontent.com/75996090/147405209-f64baa15-d767-4135-801e-b62907af53d0.png)
#### Ghép lại được https://karenskitchen101286359.wordpress.com/hidden_palace chứa nửa flag còn lại
![image](https://user-images.githubusercontent.com/75996090/147405243-fc7ae4d0-48cc-4a1a-baa8-b6d8f4c311ff.png)
### Flag5: CSFLAG5_CM2021{g00d_pr0bl3m_s0lv3r_th3_l3g4nd_47}

#### Nội dụng [paste thứ 2](https://pastebin.com/K0GV2ET3) với password là karen
![image](https://user-images.githubusercontent.com/75996090/147406184-c759a644-054a-4c68-8cdc-c810a6f0f8a2.png)
#### Decode mã morse được message: `the initial letter of all the posts, from oldest to newest`. Ý là bạn phải kết hợp các chữ cái đầu tiên trong các bài blog của Karen từ cũ nhất đến mới nhất.
#### Đây là tất cả blog https://karenskitchen101286359.wordpress.com/author/karendouche1412/
![image](https://user-images.githubusercontent.com/75996090/147406277-ef1e2704-a005-44ec-a10c-c2b05f242c0a.png)
#### Ban đầu mình hơi ngu vì mình lại đi kết hợp chữ p trong từ Protected để tạo thành hiplep. Sau hint thì mình mới nhận ra và làm lại, từ đúng phải là `hitler`
#### Tiếp tục nhận được một hidden protected site nữa: https://karenskitchen101286359.wordpress.com/hitler. Password ở đây là `deathtoSanta` nhận được từ paste 2
#### Mở kho báu và lấy flag8 thôi :))
![image](https://user-images.githubusercontent.com/75996090/147406425-43cd88fa-ca27-4700-957f-31a6e68055e1.png)
### Flag 8: CSFLAG8_CM2021{ZuP3rb_h4kk3r_m4N}
## End
#### Trong writeup này mình ko nhắc đến nhưng lần mình bị rickroll do nó có [QUÁ NHIỀU](https://bit.ly/3Ji8OMq), đặc sản của Cyber Space 🙂 
#### Nhưng dù sao cũng cảm ơn CS vì một Noel tuyệt vời với gần 2 ngày trời ngồi trước màn hình máy tính để giải challenge =]]]]
#### Cũng hi vọng các bạn sẽ học được gì đó từ write-up này ~~(nếu thấy hay cho mình xin star🌟, subcribe và donate nhé)~~
### Thanks for reading!!!
