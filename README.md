# Brook for port forwarding 

# 准备工作
  * VPS一台  
  * Centos7系统，防火墙已经设置好，参考 https://github.com/stardock/fwd
  
# 下载程序  
 * brook的github仓库  
 `https://github.com/txthinking/brook`  
 
 * 直接wget相关下载链接，得到一个可执行文件  
 `wget https://github.com/txthinking/brook/releases/download/v20190601/brook`  
 
 * 拷贝到bash路径下  
 `cp brook /usr/bin/`  
 
 * 给予可执行权限  
 `chmod +x /usr/bin/brook`  
 
 



    
    
    
    brook的github仓库：
https://github.com/txthinking/brook

部署服务端：

搭建方法非常简单，直接wget相关下载链接，得到一个可执行文件
wget https://github.com/txthinking/brook/releases/download/v20181212/brook
#我的vps是64位的Linux，所以下载这个

cp brook /usr/bin/
#拷贝到bash路径下

chmod +x /usr/bin/brook
#给予可执行权限

使用方法：
brook -h  #帮助
brook server -l :端口号 -p 密码  #启动服务
​


设置开机自动启动：

vi /etc/systemd/system/brook.service

粘贴以下内容:
[Unit]
Description = This will run at startup

[Service]
ExecStart = /usr/bin/brook service -l :9999 -p 1234qwer

[Install]
WantedBy = multi-user.target

粘贴完后赋予可执行权限
chmod +x /etc/systemd/system/brook.service
设置开机自动启动
systemctl enable /etc/systemd/system/brook.service




多端口启动

    # 启动 多个端口转发
    # 分别为：
    #     监听端口 2333，被转发的服务器IP为 2.2.2.2 端口为 6666
    #     监听端口 6666，被转发的服务器IP为 3.3.3.3 端口为 6688
    #     监听端口 8888，被转发的服务器IP为 6.6.6.6 端口为 7766
     
    nohup ./brook relays -l ":2333 2.2.2.2:6666" -l ":6666 3.3.3.3:6688" -l ":8888 6.6.6.6:7766" > /dev/null 2>&1 &
