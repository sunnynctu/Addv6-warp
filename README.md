
#### 为IPV4服务器添加WARP IPV6，脚本主要针对IPV4 only VPS，添加WARP IPV6网络支持，增加几个支持ipv6的DNS服务器（谷歌、阿里）
**####修改后的小鸡可访问ipv6资源，也可作为ipv4 only环境下连接ipv6 only机器的跳板机，亲测可在ipv4环境中连接EUserv**
**####默认已设置小鸡自带的IPV4优先，仅访问ipv6时启用通过WARP，为Cloudflare WARP节省资源**



-------------------------------------------------------------------------------------------------------


##### Debian 10/Ubuntu 20.04系统脚本,一键到底！
```
wget -qO- https://cdn.jsdelivr.net/gh/sunnynctu/Addv6-warp/WARP6.sh|bash
```

##### 搞定,输入以下命令查看是否获得ipv6地址，尝试跳板连接你的ipv6 only 小鸡吧
```
curl -6 ip.p3terx.com
```
------------------------------------------------------------------------------------------------------------- 
##### 分流配置文件(以下默认全局IPV4优先，还可设置全局IPV6、分流IPV4优先域名、分流IPV6优先域名，共4种情况，详情见视频教程)
```
{ 
"outbounds": [
    {
      "tag":"IP6-out",
      "protocol": "freedom",
      "settings": {}
    },
    {
      "tag":"IP4-out",
      "protocol": "freedom",
      "settings": {
        "domainStrategy": "UseIPv4" 
      }
    }
  ],
  "routing": {
    "rules": [
      {
        "type": "field",
        "outboundTag": "IP4-out",
        "domain": [""] 
      },
      {
        "type": "field",
        "outboundTag": "IP6-out",
        "network": "udp,tcp" 
      }
    ]
  }
}
``` 
 ---------------------------------------------------------------------------------------------------------

#### 相关WARP进程命令

手动临时关闭WARP网络接口
```
wg-quick down wgcf
```
手动开启WARP网络接口 
```
wg-quick up wgcf
```

查看WARP当前统计状态
```
wg
```

启动systemctl enable wg-quick@wgcf

开始systemctl start wg-quick@wgcf

重启systemctl restart wg-quick@wgcf

停止systemctl stop wg-quick@wgcf

关闭systemctl disable wg-quick@wgcf

#### 下期彩蛋：EUserv双栈warp？可以有！

---------------------------------------------------------------------------------------------------------------------

感谢P3terx及原创者们，参考来源：
 
https://p3terx.com/archives/debian-linux-vps-server-wireguard-installation-tutorial.html

https://p3terx.com/archives/use-cloudflare-warp-to-add-extra-ipv4-or-ipv6-network-support-to-vps-servers-for-free.html

https://luotianyi.vc/5252.html
