# [极客大挑战 2019]PHP

[Link](https://buuoj.cn/challenges#[%E6%9E%81%E5%AE%A2%E5%A4%A7%E6%8C%91%E6%88%98%202019]PHP)

Đầu tiên, khi mình boot instance và truy cập vào challenge, mình cảm thấy rất bất ngờ với giao diện của trang web. Mình nghĩ rằng author đã làm việc rất chăm chỉ.
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

