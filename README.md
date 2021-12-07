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

