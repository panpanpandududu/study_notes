#### 1.文件名或路径名包含中文时，git status显示乱码

当文件名和路径名包含中文时，git status 显示为乱码

![1548320753988](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1548320753988.png)

此时解决此问题，只需告诉git不对OX80以上的字符进行转义即可：

`$ git config --global core.quotepath false`

