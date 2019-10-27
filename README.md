# Pingtunnel
pingtunnel是把udp流量伪装成icmp流量进行转发的工具，类似于kcptun。用于突破网络封锁，或是绕过WIFI网络的登陆验证，或是在某些网络加速网络传输速度。
<br />Pingtunnel is a tool that advertises udp traffic as icmp traffic for forwarding, similar to kcptun. Used to break through the network blockade, or to bypass the WIFI network login verification, or speed up network transmission speed on some networks. 

![image](network.png)

# Sample
如把本机的:4455的UDP流量转发到www.yourserver.com:4455：For example, the UDP traffic of the machine: 4545 is forwarded to www.yourserver.com:4455:
* 在www.yourserver.com的服务器上用root权限运行。Run with root privileges on the server at www.yourserver.com
```
sudo ./pingtunnel -type server
```
* 在你本地电脑上用管理员权限运行。Run with administrator privileges on your local computer
```
pingtunnel.exe -type client -l :4455 -s www.yourserver.com -t www.yourserver.com:4455
```
* 如果看到客户端不停的ping、pong日志输出，说明工作正常。If you see the client ping, pong log output, it means normal work
```
ping www.xx.com 2018-12-23 13:05:50.5724495 +0800 CST m=+3.023909301 8 0 1997 2
pong from xx.xx.xx.xx 210.8078ms
```
* 如果想转发tcp流量，只需要在客户端加上-tcp的参数。If you want to forward tcp traffic, you only need to add the -tcp parameter to the client.
```
pingtunnel.exe -type client -l :4455 -s www.yourserver.com -t www.yourserver.com:4455 -tcp 1
```
# Usage

    通过伪造ping，把tcp/udp流量通过远程服务器转发到目的服务器上。用于突破某些运营商封锁TCP/UDP流量。
    By forging ping, the tcp/udp traffic is forwarded to the destination server through the remote server. Used to break certain operators to block TCP/UDP traffic.

    Usage:

    pingtunnel -type server

    pingtunnel -type client -l LOCAL_IP:4455 -s SERVER_IP -t SERVER_IP:4455 -tcp 1

    -type     服务器或者客户端
              client or server

    -l        本地的地址，发到这个端口的流量将转发到服务器
              Local address, traffic sent to this port will be forwarded to the server

    -s        服务器的地址，流量将通过隧道转发到这个服务器
              The address of the server, the traffic will be forwarded to this server through the tunnel

    -t        远端服务器转发的目的地址，流量将转发到这个地址
              Destination address forwarded by the remote server, traffic will be forwarded to this address

    -timeout  本地记录连接超时的时间，单位是秒，默认60s
              The time when the local record connection timed out, in seconds, 60 seconds by default

    -key      设置的密码，默认0
              Set password, default 0

    -tcp      设置是否转发tcp，默认0
              Set the switch to forward tcp, the default is 0

    -tcp_bs   tcp的发送接收缓冲区大小，默认10MB
              Tcp send and receive buffer size, default 10MB

    -tcp_mw   tcp的最大窗口，默认10000
              The maximum window of tcp, the default is 10000

    -tcp_rst  tcp的超时发送时间，默认400ms
              Tcp timeout resend time, default 400ms

	-tcp_gz   当数据包超过这个大小，tcp将压缩数据，0表示不压缩，默认0
              Tcp will compress data when the packet exceeds this size, 0 means no compression, default 0

    -nolog    不写日志文件，只打印标准输出，默认0
              Do not write log files, only print standard output, default 0 is off
