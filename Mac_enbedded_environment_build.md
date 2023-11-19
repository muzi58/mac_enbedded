转自作者：五街教授 https://www.bilibili.com/read/cv18942590/?spm_id_from=333.999.0.0 出处：bilibili
# MAC 51单片机开发环境 

# 1. Homebrew包管理工具安装 

## 1.1 什么是homebrew

homebrew是MacOS系统里面包的管理工具，主要解决软件或者包下载时的各种依赖包。 

## 1.2 homebrew 下载安装

运行下面命令

/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

出现 ![img](https://i0.hdslb.com/bfs/article/7c8dfe70d959c1cb98a057cd9dc9815097b28fe1.png@1256w_300h_!web-article-pic.avif)

选择1（中科大的下载源）

安装成功后，运行 brew -v ![img](https://i0.hdslb.com/bfs/article/9afa79a17b88f82d253f5b1acfb95f480121e7c3.png@1256w_216h_!web-article-pic.avif)

# 2. 搭建vscode 51单片机开发环境 

## 2.1 在vscode中安装PlatformIO IDE 

![img](https://i0.hdslb.com/bfs/article/e3883a6a847b7b8097cdbb1111decd4b161c60d2.png@1256w_984h_!web-article-pic.avif)

## 2.2 创建工程 

![img](https://i0.hdslb.com/bfs/article/9f09115e3463c7cbfb5bfb10db1b0b22c3acabe2.png@1256w_422h_!web-article-pic.avif)

新建51工程 

![img](https://i0.hdslb.com/bfs/article/9faee49de7c98ed0914471f393b003fe68699bf3.png@1256w_508h_!web-article-pic.avif)

工程文件生成，并创建c文件 ![img](https://i0.hdslb.com/bfs/article/d5040b9818819a126186c7c8fb54da874db9f039.png@1256w_1066h_!web-article-pic.avif)

消除错误，编辑c_cpp_properties.json， 找到我们c51的头文件路径。我的是在

/Users/xuchuanlei/.platformio/packages/toolchain-sdcc/share/sdcc/include/ 

![img](https://i0.hdslb.com/bfs/article/c337b7b01639ab05ad60af14c01b6f66d031a89f.png@1256w_964h_!web-article-pic.avif)

编译代码 command+shift+b 快捷键 

![img](https://i0.hdslb.com/bfs/article/5787c4edae4e28285375772feb775fb6c48711c0.png@1256w_290h_!web-article-pic.avif)



# 3. CH340串口驱动安装

官方没有mac 版本的ch340的驱动，但是ch341是兼容ch340的，所以我们去官网去下载ch341的驱动。

下载地址：https://www.wch.cn/download/CH341SER_MAC_ZIP.html

安装过程，一路下一步即可。但是要注意，可能有权限问题。

去mac设置中的安全中心放开权限。

安装完成后，连接上板子，发送 ls /dev/cu.wchus*,应该就会有设备。

# 4. stcgal 安装

github 地址：https://github.com/grigorig/stcgal

官方有两种方式安装，但是要求先有python 环境。homebrew 安装python比较简单，直接运行命令brew install python即可。

配置python 环境变量,在.bash_profile中添加以下alias python="/usr/bin/python3"

brew install python vi ~/.bash_profile #将alias python="/usr/bin/python3" 添加到文件中 source ～/.bash_profile

两种方式安装stcgal

pip3 install stcgal

在github 地址中下载某个taget节点下的zip包.执行./setup.py build 编译，然后执行./setup.py install 来安装

stcgal -V



下载程序到开发板。

开发版连接到电脑上之后，在终端输入 ls /dev/cu.wchus* 

![img](https://i0.hdslb.com/bfs/article/311b5c3325b5329733c00afd9005727a6b3324bf.png@!web-article-pic.avif)

可以看到，我们当前的设备。

stcgal -P stc89 -p /dev/cu.wchusbserial1120 firmware.hex

![img](https://i0.hdslb.com/bfs/article/b2da2273aca03d5187af5cb3ca769db2277cafb2.png@1256w_112h_!web-article-pic.avif)

将开发板断电重连，即可出现下面的打印

![img](https://i0.hdslb.com/bfs/article/a8107661028b97069335e3fa9ecba3fdee63fcdf.png@1256w_650h_!web-article-pic.avif)

至此，我们将我们的编译的代码下载到开发板中了。

![img](https://i0.hdslb.com/bfs/article/0c6fce15d143fb243a7784c891bd9bc133e3338e.jpg@1256w_1676h_!web-article-pic.avif)





