# [极客大挑战 2019]BuyFlag
[Link](https://buuoj.cn/challenges#[%E6%9E%81%E5%AE%A2%E5%A4%A7%E6%8C%91%E6%88%98%202019]BuyFlag)

Sau khi boot instance, mình truy cập vào `http://e1271b35-ce49-478f-86a8-932dd887283f.node4.buuoj.cn:81/pay.php` và thấy gợi ý để buy flag

![image](https://user-images.githubusercontent.com/95614411/173813875-c6dad6b4-bf36-4149-b52e-71e49626cf05.png)

Đầu tiên, mình check cookie và chỉnh value của `user` từ `0` thành `1`.

![image](https://user-images.githubusercontent.com/95614411/173814100-491eff95-ef51-4df6-9782-5c2d9160b159.png)

Kế tiếp, mình xem source và phát hiện một đoạn code khá thú vị.

![12345](https://user-images.githubusercontent.com/95614411/173814746-9b135562-2126-4565-b0af-10d214c42312.png)


Và, mình phải tìm cách bypass qua function `is_numeric()`. Và cũng có khá nhiều cách bypass, ví dụ như:

```
?password = 404%00
?password = 404%20
?password = 404'
?password = 404a
?password = 404+
```
Để tìm hiểu rõ hơn thì [vào đây](https://chowdera.com/2022/01/202201160540112886.html)
Và, mình cần post lên 1 query string money, nhưng mình gặp phải vấn đề:

![image](https://user-images.githubusercontent.com/95614411/173815515-99adcf58-312f-42c1-9744-9fab1a044198.png)

Mình tìm hiểu, và chỉnh lại payload như sau: `password=404+&money=10e10`
Và kết quả
![image](https://user-images.githubusercontent.com/95614411/173815726-5fa9b482-e620-41a0-a62f-b8fdd553c01e.png)

### Thanks for reading
