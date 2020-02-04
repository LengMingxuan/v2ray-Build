# v2ray-Build

![](https://img.shields.io/badge/Demo%20for-macOS-blue)      ![](https://img.shields.io/badge/Suitable%20for-Full%20platform-yellow)     ![](https://img.shields.io/badge/Platform-Google%20Cloud-green?style=flat&logo=Google-Cloud)    ![](https://img.shields.io/badge/based%20on-CentOS-green?style=flat&logo=CentOS&logoColor=yellow)

Use simple and easy-to-understand sentences to teach you how to set up v2ray on a web server to access the Internet

> 本教程中使用的软件来自macOS，Windows请根据其他三方软件进行使用（具体使用方式应该类似）

> 本教程使用的‘$指令’ 在CentOS 7 下可正常使用，如果小白用户新建服务器时可以直接选择跟我一样的版本

> !!!本教程默认你已经创建好了可以访问外网的服务器


### 1.安装wget

在登录完成的窗口输入以下命令并回车进行wget安装：

```$
yum -y install wget
```

### 2.下载脚本

安装完wget之后就可以进行下载v2ray的脚本了，输入如下命令并回车：

```$
wget https://install.direct/go.sh
```
### 3.安装unzip

因为centos不支持apt-get，我们需要安装unzip，详见官方说明：

```$
yum install -y zip unzip  
```
### 4.执行安装

输入下面的命令并回车执行安装
```$
bash go.sh 
```
在首次安装完成之后，V2Ray不会自动启动，需要手动运行上述启动命令。
```
## 启动
systemctl start v2ray

## 停止
systemctl stop v2ray

## 重启
systemctl restart v2ray

## 开机自启
systemctl enable v2ray
```

### 5.安装nano
我习惯用nano文本编辑器
```$
yum -y install nano
```

### 6.修改默认端口
```默认
nano /etc/v2ray/config.json
```
你会看到这些内容，光标移动到第二行“port”将后面的14670默认端口改成你想改的端口，我这改的是8848，然后按`ctrl+X`，再按`Y`，再敲`回车`保存
```

  "inbounds": [{
    "port": 14670,
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "1d35af37-4f96-4f15-9f32-2281a342bc5f",
          "level": 1,
          "alterId": 64
        }
      ]
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  },{
    "protocol": "blackhole",
    "settings": {},
    "tag": "blocked"
  }],
  "routing": {
    "rules": [
      {
        "type": "field",
        "ip": ["geoip:private"],
        "outboundTag": "blocked"
      }
    ]
  }
}
```
到此服务器方面的配置就结束了，不过要注意一点在你的服务器管理页面中需要开启你刚才设置的端口！！！

## 客户端配置
![](https://github.com/LengMingxuan/My-Image-Hosting-Service/blob/master/img/%E6%88%AA%E5%B1%8F2020-02-04%E4%B8%8A%E5%8D%8810.32.13.png?raw=true)

先点击`加号`添加一个节点，然后再内容内输入你刚才的参数，再服务器终端内输入：
```$
cat /etc/v2ray/config.json
```
然后填进去就行了。
