### 个人使用Debian的常用功能

#### 设置系统环境变量设置网络代理
```bash
export http_prxy="http://"  #配置代理服务器地址
export https_proxy="http://"

source /etc/environment # 手动加载环境变量配置
```
如果只是为某个用户配置网络代理，可以在该用户的.bashrc或者.basn_profile添加如下配置
#### 单独为某个服务设置网络代理
```bash
sudo mkdir -p /etc/systemd/system/docker.service.d          # 为Docker服务创建单独的配置文件夹
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf #为其创建单独的网络代理配置文件
sudo systemctl daemon-reload #重新加载Systemd文件
sudo systemctl restart docker #重新启动Docker服务
```
具体的内容如下
```bash
[Service]
Environment="HTTP_PROXY=http://"
Environment="HTTPS_PROXY=http://"
```
#### 为Apt包管理器配置网络代理
```bash
sudo nanao /etc/apt/apt.conf
```
具体的配置内容如下
```
Acquire:http::proxy "http://"
Acquire:http::proxy "http://"
```
#### 配置无线网络
Debian使用NetworkManager进行网络管理  
主要使用nmcli(命令行方式进行网络管理)和nmtui(可视化界面进行网络管理)进行网络管理