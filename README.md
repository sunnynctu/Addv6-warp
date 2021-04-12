
#### 为IPV4服务器添加WARP IPV6，脚本主要针对IPV4 only VPS，添加WARP IPV6网络支持，可作为ipv4 only环境下连接ipv6 only机器的跳板机，亲测可在ipv4环境中连接EUserv
####默认已设置WARP IPV4优先



-------------------------------------------------------------------------------------------------------


##### Debian 10/Ubuntu 20.04系统脚本,一键到底！
```
wget -qO- https://cdn.jsdelivr.net/gh/sunnynctu/EUserv-addv6-warp/WARP6.sh|bash
```

##### 三、搞定,尝试连接你的ipv6 only 小鸡吧

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

感谢P3terx、YG-tsj及原创者们，参考来源：
 
https://p3terx.com/archives/debian-linux-vps-server-wireguard-installation-tutorial.html

https://p3terx.com/archives/use-cloudflare-warp-to-add-extra-ipv4-or-ipv6-network-support-to-vps-servers-for-free.html

https://luotianyi.vc/5252.html
