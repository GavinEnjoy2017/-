近日在Ubuntu上部署FTP服务器，想来记录一下过程。

1. 需要有一台服务器，例如虚拟机或者云服务器都可以，本次就用云服务器部署，首先下载FTP服务器
    `sudo apt-get install vsftpd -g`

2. 下载完成之后需要编辑FTP的配置文件,`sudo vim /etc/vsftpd.conf`,修改如下：
    ```
    listen=NO                 //是否开启监听ipv4和ipv6数据
    listen_ipv6=YES          //是否开启监听ipv6数据

    anonymous_enable=NO      //是否允许匿名登陆，无需密码

    local_enable=YES        //是否允许本地用户登录

    write_enable=YES        //是否允许登陆者上传文件

    local_umask=022         //设置本地用户默认要减免的权限

    dirmessage_enable=YES       //目录消息，能够给远程登陆的用户发送目录

    use_localtime=YES           //服务器所展示的目录将随着本地时间而改变

    xferlog_enable=YES          //开启上传下载的日志记录

    connect_from_port_20=YES    //确认连接传输的端口号为20

    xferlog_file=/var/log/vsftpd.log    //日志文件存放位置

    xferlog_std_format=YES          //日志文件采用标准格式

    ftpd_banner=Welcome to FTP service.  //在使用shell时登陆那么会发送欢迎语

    chroot_local_user=YES        //对本地用户是否实施限制
    chroot_list_enable=YES       //开启限制白名单

    chroot_list_file=/etc/vsftpd.chroot_list        //白名单路径，若无这个文件需要自己创建

    secure_chroot_dir=/var/run/vsftpd/empty

    pam_service_name=ftp            //此处ubuntu的系统需要改为ftp

    rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
    rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
    ssl_enable=NO

    utf8_filesystem=YES       //编码统一为utf8编码，可以识别中文，防止乱码
    ```
    上面配置尤其重要，如果无法访问十有八九是配置文件问题

3. 创建用户访问：
    ```
    sudo groupadd ftpusers  //创建Group用户组

    sudo useradd -m **username** //创建用户名

    sudo passwd username //创建密码

    cd /var/ftp/
    mkdir /blog   在/var/ftp 下创建blog文件夹

    chown -R username:username /var/ftp/blog  //赋予用户可以访问文件夹的权限
    ```

4. 将用户添加到白名单中，vim /etc/vsftpd.chroot_list, Ubuntu下没有这个文件首先需要创建这个文件
    ```
    sudo touch vsftpd.chroot_list
    文件内容：
    username //添加一个用户名即可
    ```

5. 重启ftp服务
    ```
    systemctl restart vsftpd
    ```

6. 按照上面方法配置成功之后就可以远程访问FTP服务器了
测试方法：
 + 可以在文件管理其中输入: ftp://ip地址
 + 在浏览器中访问: ftp:// ip地址
 + 在cmd中访问： ftp ip地址