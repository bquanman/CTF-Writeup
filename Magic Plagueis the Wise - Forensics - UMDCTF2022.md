# Magic Plagueis the Wise
>## Description: 
>Did you ever hear the tragedy of Darth Plagueis The Wise? It's written here in a magical way, but I can't figure out how to read it. Can you help me?
><br>Download file: https://drive.google.com/file/d/1Yq5ckdzTmoUEnsyLzMJYTKLdz7JEw_ve/view?usp=sharing
><br>Author: matlac<br>
>Solves: 71/553

# Solver:
#### Đề bài cho ta một file zip bên trong có 4464 file không có phần mở rộng (nhìn lượng file khá choáng :3)<br><br>![image](https://user-images.githubusercontent.com/75996090/157237826-f156f2ff-100c-4500-afb2-d1c528eb528a.png)
#### Kiểm tra loại tệp bằng `file` cũng không giúp ích được gì vì phần Magic byte đã bị sửa đổi
```
$ file 1
1: data
```
#### Dùng `hexedit` để kiểm tra mình thấy tất cả các file đều là file PNG nhưng đều bị sai magic byte đầu tiên 
```
$ hexedit 1
00000000   44 50 4E 47  0D 0A 1A 0A  00 00 00 0D  49 48 44 52  00 00 03 20  00 00 01 C1  DPNG........IHDR... ....
00000018   08 06 00 00  00 91 F7 DF  66 00 00 20  00 49 44 41  54 78 5E EC  5D 09 FC 56  ........f.. .IDATx^.]..V
00000030   C3 FA FF 0E  45 B6 12 11  8A 28 91 9D  2C 37 72 ED  4B B6 C8 1A  3F 72 2D 11  ....E....(..,7r.K...?r-.
00000048   D9 C9 52 96  4B B2 E5 22  44 64 F9 8B  08 91 5D AE  7D 89 AC B9  88 48 96 E8  ..R.K.."Dd....].}....H..
00000060   5E 25 22 B2  85 F9 7F BE  33 67 DE 33  E7 9C 39 67  CE BB FD 96  BC F3 B9 F7  ^%".....3g.3..9g........
00000078   A3 DF 7B 66  79 E6 99 ED  D9 1F 81 5A  A9 61 A0 86  81 1A 06 6A  18 A8 61 A0  ..{fy......Z.a.....j..a.
00000090   86 81 1A 06  6A 18 A8 61  A0 86 81 1A  06 EA 09 03  02 80 AC A7  B1 4A 1A 46  ....j..a.............J.F
```
```
$ hexedit 2
00000000   69 50 4E 47  0D 0A 1A 0A  00 00 00 0D  49 48 44 52  00 00 03 20  00 00 01 C1  iPNG........IHDR... ....
00000018   08 06 00 00  00 91 F7 DF  66 00 00 20  00 49 44 41  54 78 5E EC  5D 09 FC 56  ........f.. .IDATx^.]..V
00000030   C3 FA FF 0E  45 B6 12 11  8A 28 91 9D  2C 37 72 ED  4B B6 C8 1A  3F 72 2D 11  ....E....(..,7r.K...?r-.
00000048   D9 C9 52 96  4B B2 E5 22  44 64 F9 8B  08 91 5D AE  7D 89 AC B9  88 48 96 E8  ..R.K.."Dd....].}....H..
00000060   5E 25 22 B2  85 F9 7F BE  33 67 DE 33  E7 9C 39 67  CE BB FD 96  BC F3 B9 F7  ^%".....3g.3..9g........
00000078   A3 DF 7B 66  79 E6 99 ED  D9 1F 81 5A  A9 61 A0 86  81 1A 06 6A  18 A8 61 A0  ..{fy......Z.a.....j..a.
00000090   86 81 1A 06  6A 18 A8 61  A0 86 81 1A  06 EA 09 03  02 80 AC A7  B1 4A 1A 46  ....j..a.............J.F
```
#### Tiến hành sửa magic byte đầu tiên thành `89` giống magic byte chuẩn của file png và thêm `.png` vào đuôi file rồi mở lại
![1](https://user-images.githubusercontent.com/75996090/157239506-402c1a94-280e-469b-b0f7-ec89ca80d604.png)
#### Sau khi sửa file thứ 2 thứ 3 đều cho ra hình như trên thì suy nghĩ đầu tiên là phải làm cách nào đó để sửa tất cả các magic byte đầu tiên của ảnh để tìm ra ảnh duy nhất có flag trong số đó. 
#### Tuy nhiên cũng có một hoài nghi là tất cả các file có dung lượng như nhau vì thế khó có thể có một bức ảnh chứa flag mà cấu trúc và dung lượng bằng các file khác.
#### Vì vậy cần thay đổi hướng đi.
#### Đó là tách chỉ lấy các byte đầu tiên của từng file rồi gộp lại.
#### Viết một đoạn bash script và đây là kết quả<br>
![image](https://user-images.githubusercontent.com/75996090/157250450-a8ed25bb-ceec-4634-aadf-a087a40d6db2.png)
### Flag: UMDCTF{d4r7h_pl46u315_w45_m461c}
