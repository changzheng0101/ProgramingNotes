# C编译环境配置

## linux + vscode

1.开启terminal  shift+crtl+t

2.sudo apt-get update  可以不做

3.sudo apt install build-essential 

4.创建文件，然后用vscode打开

>测试： gdb --version / g++ --version

5.写main.c

crtl+shift+b 尝试编译

6.点击齿轮，会自动创建一个vscode配置文件

![image-20220126120200405](../../md_img/Linux下配置C/image-20220126120200405.png)

最后改成default

7.F5 生成launch.json 先gdb 之后default

program---生成可执行文件的路径

preLaunchTask---之前的task的label

