- 安装debian系统
  - debian 11 iso镜像下载：https://cdimage.debian.org/cdimage/archive/11.7.0/amd64/iso-dvd/
  - 问题1  apt-get报错：“Media change: please insert the disc labeled ...”   
    解决办法：https://www.pqs.pw/knowledgebase/5/-Debian-82-apt-get--Media-change-please-insert-the-disc-labeled--.html
  - 添加源报错The following signatures couldn't be verified because the public key is not available  
    https://www.cnblogs.com/FengGeBlog/p/15567119.html
         
- 安装casaos(docker会自动安装)
  - `curl -fsSL https://get.casaos.io | sudo bash`
  - `casaos -v`

- casaos需桌面环境
  - sudo apt install gnome-core 或 sudo apt install gnome
  - gnome-core：最基本的 gnome 桌面环境，包含的软件少；gnome：包含了 gnome-core ，同时添加了非常多的常用软件
  - gnome自启动 `sudo systemctl set-default graphical.target`
  - 安装chrome https://blog.csdn.net/u013541325/article/details/123922717
    
- 内网穿透2种方式
  - `tailscale` https://www.bilibili.com/video/BV1sx4y1U7Jw/?vd_source=17424b668626d148f3b05d7cf3184f2c
  - `cpolar` https://blog.csdn.net/asdssadddd/article/details/139154773
  - 几种方式的区别 https://www.liyao2018.com/post/%E5%86%85%E7%BD%91%E7%A9%BF%E9%80%8F/
 
- 问题
  - Casaos应用无法安装 docker镜像无法拉取问题
    ```
    sudo tee /etc/docker/daemon.json <<-'EOF'
    {
     "registry-mirrors": [
          "http://nb-docker.langlangy.net",
          "https://docker.m.daocloud.io",
          "https://docker.nju.edu.cn",
          "https://dockerproxy.com"
     ]
    }
    EOF
        
    sudo systemctl daemon-reload
    
    sudo systemctl restart docker
    
    ```
