### L34K
![image](https://user-images.githubusercontent.com/75996090/208494445-cce4040e-455b-41b9-8466-6ae8b1bcc76e.png)

Đề bài cho chúng ta một file crash dump, và với dung lượng lớn thế kia thì có thể đây là một file complete dump.

![image](https://user-images.githubusercontent.com/75996090/208495452-c9c1e8ee-2674-4099-a32a-d16b35223317.png)

Sử dụng vol3 để xem các tiến trình đang chạy

```bash
$ vol3.py -f MEMORY.DMP windows.pstree
Volatility 3 Framework 2.3.0
Progress:  100.00               PDB scanning finished
PID     PPID    ImageFileName   Offset(V)       Threads Handles SessionId       Wow64   CreateTime      ExitTime

4       0       System  0xa8037d0a8040  162     -       N/A     False   2022-11-19 11:24:39.000000      N/A
* 1664  4       MemCompression  0xa80381a5e040  26      -       N/A     False   2022-11-19 11:24:49.000000      N/A
* 92    4       Registry        0xa8037d081080  4       -       N/A     False   2022-11-19 11:24:30.000000      N/A
* 308   4       smss.exe        0xa8037dba7080  2       -       N/A     False   2022-11-19 11:24:39.000000      N/A
436     428     csrss.exe       0xa8037f292140  12      -       0       False   2022-11-19 11:24:42.000000      N/A
512     504     csrss.exe       0xa8037f7b7140  14      -       1       False   2022-11-19 11:24:43.000000      N/A
520     428     wininit.exe     0xa8037f7b8080  3       -       0       False   2022-11-19 11:24:43.000000      N/A
* 672   520     lsass.exe       0xa803816380c0  9       -       0       False   2022-11-19 11:24:43.000000      N/A
* 652   520     services.exe    0xa8037f762080  8       -       0       False   2022-11-19 11:24:43.000000      N/A
** 396  652     svchost.exe     0xa803817ce2c0  74      -       0       False   2022-11-19 11:24:46.000000      N/A
*** 5376        396     WMIADAP.exe     0xa80385176340  6       -       0       False   2022-11-19 12:40:35.000000     N/A
*** 3400        396     BraveUpdate.ex  0xa8038255b080  6       -       0       True    2022-11-19 11:25:05.000000     N/A
*** 4044        396     sihost.exe      0xa8038194c240  20      -       1       False   2022-11-19 11:25:05.000000     N/A
*** 3376        396     taskhostw.exe   0xa8038255c080  10      -       1       False   2022-11-19 11:25:05.000000     N/A
*** 3032        396     MicrosoftEdgeU  0xa803824c40c0  5       -       0       True    2022-11-19 11:25:05.000000     N/A
** 1036 652     svchost.exe     0xa8038182f2c0  15      -       0       False   2022-11-19 11:24:47.000000      N/A
** 2444 652     VGAuthService.  0xa80381f36300  4       -       0       False   2022-11-19 11:24:52.000000      N/A
** 784  652     svchost.exe     0xa80381694240  27      -       0       False   2022-11-19 11:24:44.000000      N/A
*** 5248        784     SystemSettings  0xa80381f11080  17      -       1       False   2022-11-19 13:05:11.000000     N/A
*** 4744        784     RuntimeBroker.  0xa80382717300  6       -       1       False   2022-11-19 11:25:14.000000     N/A
*** 7180        784     ApplicationFra  0xa803820af080  11      -       1       False   2022-11-19 13:04:51.000000     N/A
*** 6036        784     smartscreen.ex  0xa80383011080  7       -       1       False   2022-11-19 11:25:29.000000     N/A
*** 6556        784     UserOOBEBroker  0xa803829dd080  6       -       1       False   2022-11-19 13:05:14.000000     N/A
*** 5152        784     WmiPrvSE.exe    0xa80382ceb080  7       -       0       False   2022-11-19 11:25:18.000000     N/A
*** 1188        784     dllhost.exe     0xa80383697240  8       -       1       False   2022-11-19 11:26:11.000000     N/A
*** 4648        784     StartMenuExper  0xa803828dd080  20      -       1       False   2022-11-19 11:25:14.000000     N/A
*** 2860        784     WmiPrvSE.exe    0xa8037d136080  10      -       0       False   2022-11-19 11:24:59.000000     N/A
*** 2488        784     MoUsoCoreWorke  0xa80383f7b340  9       -       0       False   2022-11-19 13:04:31.000000     N/A
*** 5048        784     RuntimeBroker.  0xa80382a9d240  13      -       1       False   2022-11-19 11:25:17.000000     N/A
*** 4920        784     SearchApp.exe   0xa8038195c2c0  52      -       1       False   2022-11-19 11:25:16.000000     N/A
*** 7900        784     RuntimeBroker.  0xa8038384d080  5       -       1       False   2022-11-19 13:04:21.000000     N/A
*** 6108        784     ShellExperienc  0xa80383b16080  17      -       1       False   2022-11-19 13:03:29.000000     N/A
*** 5856        784     RuntimeBroker.  0xa80382f63080  6       -       1       False   2022-11-19 11:25:24.000000     N/A
*** 1260        784     explorer.exe    0xa80382cf4080  8       -       1       False   2022-11-19 12:40:01.000000     N/A
*** 6640        784     TextInputHost.  0xa803830d0080  15      -       1       False   2022-11-19 11:25:59.000000     N/A
*** 5620        784     RuntimeBroker.  0xa8038518f080  7       -       1       False   2022-11-19 13:03:30.000000     N/A
*** 5236        784     WinStore.App.e  0xa80383339300  11      -       1       False   2022-11-19 13:04:51.000000     N/A
** 912  652     svchost.exe     0xa8038171f2c0  11      -       0       False   2022-11-19 11:24:45.000000      N/A
** 7188 652     svchost.exe     0xa80383ebc2c0  5       -       0       False   2022-11-19 12:39:04.000000      N/A
** 1176 652     svchost.exe     0xa8038189f2c0  23      -       0       False   2022-11-19 11:24:47.000000      N/A
** 2072 652     svchost.exe     0xa80381c51080  6       -       0       False   2022-11-19 11:24:50.000000      N/A
** 2456 652     vmtoolsd.exe    0xa80381f37080  11      -       0       False   2022-11-19 11:24:52.000000      N/A
** 4252 652     svchost.exe     0xa803827052c0  7       -       1       False   2022-11-19 11:25:09.000000      N/A
** 1568 652     svchost.exe     0xa80381c4e2c0  10      -       0       False   2022-11-19 11:24:50.000000      N/A
** 3616 652     NisSrv.exe      0xa803825a6080  5       -       0       False   2022-11-19 11:25:05.000000      N/A
** 8096 652     svchost.exe     0xa80382283080  6       -       0       False   2022-11-19 12:40:13.000000      N/A
** 7460 652     svchost.exe     0xa803853972c0  8       -       0       False   2022-11-19 12:39:05.000000      N/A
** 1836 652     svchost.exe     0xa80381c4c0c0  14      -       0       False   2022-11-19 11:24:50.000000      N/A
** 2476 652     MsMpEng.exe     0xa80381f39300  33      -       0       False   2022-11-19 11:24:52.000000      N/A
** 3248 652     msdtc.exe       0xa803820f7280  12      -       0       False   2022-11-19 11:25:00.000000      N/A
** 1204 652     svchost.exe     0xa803818672c0  4       -       0       False   2022-11-19 11:24:47.000000      N/A
** 1332 652     svchost.exe     0xa803819bd2c0  18      -       0       False   2022-11-19 11:24:48.000000      N/A
** 2228 652     svchost.exe     0xa80381e2f2c0  5       -       0       False   2022-11-19 11:24:51.000000      N/A
** 1720 652     svchost.exe     0xa80381ac12c0  16      -       0       False   2022-11-19 11:24:49.000000      N/A
** 3128 652     svchost.exe     0xa8037d11c080  7       -       0       False   2022-11-19 11:24:59.000000      N/A
** 2108 652     svchost.exe     0xa80381c60200  6       -       0       False   2022-11-19 11:24:50.000000      N/A
** 2364 652     svchost.exe     0xa80381eac200  12      -       0       False   2022-11-19 11:24:52.000000      N/A
** 6220 652     svchost.exe     0xa80383fed2c0  7       -       0       False   2022-11-19 12:38:34.000000      N/A
** 1232 652     WUDFHost.exe    0xa803818d60c0  8       -       0       False   2022-11-19 11:24:47.000000      N/A
** 4820 652     SearchIndexer.  0xa803828e1240  21      -       0       False   2022-11-19 11:25:15.000000      N/A
** 736  652     svchost.exe     0xa803817d3240  18      -       0       False   2022-11-19 11:24:46.000000      N/A
*** 3548        736     ctfmon.exe      0xa8038255a080  13      -       1       False   2022-11-19 11:25:05.000000     N/A
*** 2700        736     dasHost.exe     0xa803820ec280  6       -       0       False   2022-11-19 11:24:58.000000     N/A
** 356  652     svchost.exe     0xa803817c9200  23      -       0       False   2022-11-19 11:24:46.000000      N/A
** 2020 652     spoolsv.exe     0xa80381baa080  9       -       0       False   2022-11-19 11:24:50.000000      N/A
** 6116 652     SecurityHealth  0xa80382d48240  10      -       0       False   2022-11-19 11:25:29.000000      N/A
** 1768 652     svchost.exe     0xa80381b4e2c0  11      -       0       False   2022-11-19 11:24:49.000000      N/A
*** 2052        1768    audiodg.exe     0xa803829cb080  4       -       0       False   2022-11-19 13:03:30.000000     N/A
** 1896 652     svchost.exe     0xa80381bb32c0  5       -       0       False   2022-11-19 11:24:50.000000      N/A
** 5352 652     SgrmBroker.exe  0xa80385355340  7       -       0       False   2022-11-19 12:38:57.000000      N/A
** 1904 652     svchost.exe     0xa80381bb4080  5       -       0       False   2022-11-19 11:24:50.000000      N/A
** 2932 652     svchost.exe     0xa80382072200  26      -       0       False   2022-11-19 11:24:55.000000      N/A
** 2164 652     dllhost.exe     0xa8037d127080  14      -       0       False   2022-11-19 11:24:59.000000      N/A
** 4084 652     svchost.exe     0xa80381bbd200  12      -       1       False   2022-11-19 11:25:05.000000      N/A
** 7156 652     svchost.exe     0xa803851812c0  9       -       0       False   2022-11-19 12:38:42.000000      N/A
** 1404 652     vm3dservice.ex  0xa80381948200  4       -       0       False   2022-11-19 11:24:48.000000      N/A
* 820   520     fontdrvhost.ex  0xa80381698140  5       -       0       False   2022-11-19 11:24:45.000000      N/A
580     504     winlogon.exe    0xa8038160c2c0  5       -       1       False   2022-11-19 11:24:43.000000      N/A
* 2888  580     userinit.exe    0xa803825fe080  0       -       1       False   2022-11-19 11:25:07.000000      2022-11-19 11:25:34.000000
** 1600 2888    explorer.exe    0xa80382669080  78      -       1       False   2022-11-19 11:25:08.000000      N/A
*** 6080        1600    SecurityHealth  0xa80382d4a080  3       -       1       False   2022-11-19 11:25:29.000000     N/A
*** 3044        1600    brave.exe       0xa80382e21080  0       -       1       False   2022-11-19 11:25:37.000000     2022-11-19 11:26:10.000000
*** 6948        1600    brave.exe       0xa803823e9080  32      -       1       False   2022-11-19 12:38:17.000000     N/A
**** 2848       6948    brave.exe       0xa80381b56080  17      -       1       False   2022-11-19 12:38:41.000000     N/A
**** 6424       6948    brave.exe       0xa80383ff2080  9       -       1       False   2022-11-19 12:38:29.000000     N/A
**** 5828       6948    brave.exe       0xa803836a42c0  21      -       1       False   2022-11-19 12:38:50.000000     N/A
**** 4388       6948    brave.exe       0xa80383a86080  15      -       1       False   2022-11-19 12:39:03.000000     N/A
**** 7172       6948    brave.exe       0xa8038519f080  15      -       1       False   2022-11-19 12:39:04.000000     N/A
**** 4232       6948    brave.exe       0xa80383a8f080  13      -       1       False   2022-11-19 12:38:17.000000     N/A
**** 6184       6948    brave.exe       0xa8038369e240  13      -       1       False   2022-11-19 12:38:18.000000     N/A
**** 7528       6948    brave.exe       0xa80383105080  16      -       1       False   2022-11-19 12:39:05.000000     N/A
**** 7592       6948    brave.exe       0xa803855e3080  15      -       1       False   2022-11-19 12:39:06.000000     N/A
**** 1644       6948    brave.exe       0xa80383d9d080  17      -       1       False   2022-11-19 12:39:01.000000     N/A
**** 4792       6948    brave.exe       0xa803831e3080  16      -       1       False   2022-11-19 12:38:19.000000     N/A
**** 7260       6948    brave.exe       0xa80385144080  15      -       1       False   2022-11-19 12:39:04.000000     N/A
**** 6128       6948    brave.exe       0xa803830ba2c0  16      -       1       False   2022-11-19 12:38:49.000000     N/A
**** 3632       6948    brave.exe       0xa80383f5d2c0  16      -       1       False   2022-11-19 12:38:49.000000     N/A
**** 3920       6948    brave.exe       0xa8038518e080  15      -       1       False   2022-11-19 12:39:04.000000     N/A
**** 6296       6948    brave.exe       0xa803822e9240  9       -       1       False   2022-11-19 12:38:18.000000     N/A
**** 5500       6948    brave.exe       0xa803828f9080  9       -       1       False   2022-11-19 12:38:17.000000     N/A
**** 7384       6948    brave.exe       0xa80385381080  15      -       1       False   2022-11-19 12:39:04.000000     N/A
*** 5544        1600    mspaint.exe     0xa80383d98080  8       -       1       False   2022-11-19 12:40:12.000000     N/A
*** 5652        1600    OneDrive.exe    0xa80383144080  25      -       1       False   2022-11-19 11:25:38.000000     N/A
**** 6544       5652    Microsoft.Shar  0xa8038266c080  0       -       1       False   2022-11-19 11:25:57.000000     2022-11-19 11:26:07.000000
*** 3160        1600    vmtoolsd.exe    0xa80382d50080  11      -       1       False   2022-11-19 11:25:30.000000     N/A
*** 5208        1600    vm3dservice.ex  0xa80382d49080  3       -       1       False   2022-11-19 11:25:30.000000     N/A
*** 380 1600    notepad.exe     0xa8038539e080  4       -       1       False   2022-11-19 12:40:33.000000      N/A
* 812   580     fontdrvhost.ex  0xa80381696080  5       -       1       False   2022-11-19 11:24:45.000000      N/A
* 1004  580     dwm.exe 0xa8038179a080  15      -       1       False   2022-11-19 11:24:46.000000      N/A
```
Phần lớn là các tiến trình của hệ thống, do bài không đề cập đến malware nên ta cũng chẳng cần đào sâu vào các tiến trình đó làm gì mà chỉ cần tập trung vào các tiến trình do người dùng tạo ra như notepad.exe, brave.exe, mspaint.exe ...

Sau khi phân tích mspaint.exe với các [thủ thuật](https://www.rootusers.com/google-ctf-2016-forensic-for1-write-up/) đã biết, mình không tìm thấy thông tin gì nên chuyển sang phân tích tiến trình brave và cụ thể là điều tra các trang web người dùng đã truy cập hoặc các file được tải xuống qua brave.

Sau khi thử cài đặt Brave và phân tích, mình thấy Brave cũng giống các trình duyệt khác là lưu lịch sử trình duyệt trong file `History` tại đường dẫn `\Local\BraveSoftware\Brave-Browser\User Data\Default\`.

![image](https://user-images.githubusercontent.com/75996090/208569184-60ab16ea-36be-41f1-b0c1-cf71d0d95008.png)

Dùng plugin filescan để tìm offset address và dump file `History` này

```bash
bquanman@BquanmanPC:/mnt/c/Users/bquanman/Desktop/CTF/ISITDTUFinal$ vol3.py -f MEMORY.DMP windows.filescan | grep History
0xa80382e6bc40.0\Windows\System32\winevt\Logs\Microsoft-Windows-FileHistory-Core%4WHC.evtx      216
0xa803836559c0  \Users\TommyXiaomi\AppData\Local\BraveSoftware\Brave-Browser\User Data\Default\History  216
0xa80383a53d10  \Users\TommyXiaomi\AppData\Local\BraveSoftware\Brave-Browser\User Data\Default\History  216

bquanman@BquanmanPC:/mnt/c/Users/bquanman/Desktop/CTF/ISITDTUFinal$ vol3.py -f MEMORY.DMP windows.dumpfiles --virtaddr 0xa803836559c0
Volatility 3 Framework 2.3.0
Progress:  100.00               PDB scanning finished
Cache   FileObject      FileName        Result

DataSectionObject       0xa803836559c0  History file.0xa803836559c0.0xa80383490ab0.DataSectionObject.History.dat
SharedCacheMap  0xa803836559c0  History file.0xa803836559c0.0xa803826dfa20.SharedCacheMap.History.vacb

bquanman@BquanmanPC:/mnt/c/Users/bquanman/Desktop/CTF/ISITDTUFinal$ file file*
file.0xa803836559c0.0xa803826dfa20.SharedCacheMap.History-1.vacb:   data
file.0xa803836559c0.0xa80383490ab0.DataSectionObject.History-1.dat: SQLite 3.x database, last written using SQLite version 3038000
```

Sử dụng DB Browser để phân tích history db

![image](https://user-images.githubusercontent.com/75996090/208569765-16680789-f60b-42c0-b36e-d81f3d4b3278.png)

Nhận được một link pastebin tuy nhiên nó được bảo vệ bằng mật khẩu. Pastebin đc sử dụng để lưu các **document** online nên đây có thể là **secret document** đề bài nhắc đến. Ngoài ra khả năng cao là mật khẩu được viết bằng **text editor** chính là notepad. Vì vậy mục tiêu còn lại là phải tìm ra chuỗi đang được viết trong notepad khi máy bị crash. 

Vì đoạn text chưa được lưu vào ổ cứng nên ta phải tìm nó trong process memory. 

Mình có thử dùng plugin `memdump` để dump notepad process và dùng strings để tìm các chuỗi trông giống mật khẩu nhưng ko thấy, bruteforce với pastebin thì cũng ko khả thi. 

Vì thế sau một số tìm kiếm thì mình hiểu là các chuỗi khi ghi vào notepad sẽ được lưu trong heaps và ta phải tìm đúng địa chỉ heap đang chứa đoạn text đó.

Cuốn [The Art Of Memory Forensics](https://repo.zenk-security.com/Forensic/The%20Art%20of%20Memory%20Forensics%20-%20Detecting%20Malware%20and%20Threats%20in%20Windows,%20Linux,%20and%20Mac%20Memory%20(2014).pdf) có giải thích cách để tìm text trong `notepad's heap` và cũng giới thiệu plugin `heaps` để hỗ trợ việc này. Tuy nhiên nó chỉ hỗ trợ các phiên bản win thấp dưới Win7 như Winxp nên ta không sử dụng được ở bài này mà phải làm thủ công. 

1. Sử dụng `WinDBG` để tìm địa chỉ notepad process `!process 0 0 notepad.exe`

![image](https://user-images.githubusercontent.com/75996090/208584358-4b7352fa-7b3f-4e6b-ad23-bd9950a114b5.png)

2. Kết nối với quy trình notepad: `.process /r /p ffffa8038539e080`

![image](https://user-images.githubusercontent.com/75996090/208584646-e5f21e11-683a-472f-a38a-01781113cabd.png)

3. Liệt kê tất cả các vùng bộ nhớ heap và tìm địa chỉ của chunk có cờ "extra"

![image](https://user-images.githubusercontent.com/75996090/208585412-b419a643-d280-4d87-9f4b-930d546680e1.png)

![image](https://user-images.githubusercontent.com/75996090/208585373-45773081-c342-478c-990c-c753ed59a1d5.png)

4. Hiển thị nội dung trong heap

![image](https://user-images.githubusercontent.com/75996090/208587538-f7343703-3dd3-4296-81dd-7b1809bf57b2.png)

=> Ta được mật khẩu `#.$2n !:n]/0`

![image](https://user-images.githubusercontent.com/75996090/208587351-e5d500f1-d495-4fce-93b1-2005addf17a1.png)

#### Flag: ISITDTU{R3c0v3r_d4t@_fr0m_H34p_m3m0Ry}
