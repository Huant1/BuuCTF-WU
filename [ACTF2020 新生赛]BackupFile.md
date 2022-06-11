# [ACTF2020 新生赛]BackupFile

[link](https://buuoj.cn/challenges#[ACTF2020%20%E6%96%B0%E7%94%9F%E8%B5%9B]BackupFile)

Sau khi boot intansce và truy cập vào chall thì mình nhận được một hint.
![image](https://user-images.githubusercontent.com/95614411/173176976-c39be439-09fd-466a-a081-399f2a6111d8.png)

Sau khi tìm tòi ngang dọc trên web mà vẫn chưa ra, mình quyết định dùng `dirsearch` để bruteforce tìm link tải về source.

> Những file lưu trữ thường có extension như sau:
![1](https://user-images.githubusercontent.com/95614411/173177108-344b843a-3fb8-411a-8f85-e0c5fa51c562.PNG)
 
Và sau một lúc tìm kiếm thì mình đã tìm ra link để download source code về.
 ![2](https://user-images.githubusercontent.com/95614411/173177138-6042b18c-7cab-441c-91f2-a13d1b576413.PNG)
 
 ![3](https://user-images.githubusercontent.com/95614411/173177159-0c7e6126-303d-49ac-86bd-fdf1d4f098d5.PNG)

[Thông tin về hàm intval](https://www.php.net/manual/en/function.intval.php)

Ở đây, ta sẽ truyền một tham số vào thông qua query string `?key=...`, và chỉ nhận mỗi tham số là số vào.

![image](https://user-images.githubusercontent.com/95614411/173177273-e1873650-3207-4433-a1e5-3f1603488a93.png)

Chý ý vào hàm so sánh, ở đây, là so sánh giữa 1 biến số nguyên và 1 biến chuỗi, vì vậy, biến chuỗi sẽ tự động chuyển về biến số nguyên. Và, tại đây thì $string=123.

payload: `http://fda98420-0c3a-47e8-8399-ae8b3e60f95b.node4.buuoj.cn:81/?key=123`

![4](https://user-images.githubusercontent.com/95614411/173177326-595298c6-26e1-4411-a627-4a74eb09d55c.PNG)


### Thanks for reading!
 
