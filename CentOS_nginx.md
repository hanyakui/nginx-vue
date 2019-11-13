# CentOS Nginx配置
 

# 1.安装nginx
```
 1.安装epel: yum install epel-release 
 2.安装nginx: sudo yum install nginx
 3.运行Nginx: sudo service nginx start
 4.查看Nginx运行状态: systemctl status nginx.service
 5.启动Nginx: 
      systemctl start nginx  #启用Nginx 
      systemctl enable nginx #设置开机启动 
```  
# 2.nginx 403问题
```
https://blog.csdn.net/qq_35843543/article/details/81561240

1.将SELINUX=enforcing 修改为 SELINUX=disabled 状态。
    vi /etc/selinux/config
    SELINUX=disabled
  reboot 后生效
```
 