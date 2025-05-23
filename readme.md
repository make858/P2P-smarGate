# samrGate（SG） 中文 | [English](https://github.com/lazy-luo/smarGate/blob/master/README_en.md)

## SG是什么？
* 是个跨网段远程端口映射工具
  * 支持内网到内网、内网到外网映射
* 是个随身携带可灵活控制访问入口的工具
  * 所有配置操作都在app客户端，一眼看全、高度安全可控
  * 访问入口既可配置到app所在手机上，也能配置到任意SG服务端电脑上
* 是个简单的远程文件管理工具
  * 可对手机及服务端所在服务器进行文件管理操作
* 是个简单的socks代理工具
* 是个简单的http(s)代理工具
* ......

## SG有什么特点？
* 所有映射都通过app客户端进行配置，服务端运行时免配置
* 支持服务端到APP及服务端到服务端的端口映射
  * 可以将服务端所在内网任意机器任意端口映射到app所在手机上，通过访问手机本地端口进行穿透访问
  * 可以通过app客户端配置，将A服务端内网任意主机任意端口映射到B服务端所在主机上
* 支持链式代理
* 支持多用户隔离
* 支持ipv4/6，基于TCP进行P2P穿透
* 支持自建代理进行数据转发
* 支持数据隧道加密（TLS）
* 支持自动数据隧道选择
  * 优先P2P，次选自定义代理，官方代理兜底
* 支持自动版本升级及APP客户端上一键升级
* socks及http(s)代理支持自定义ip白名单及域名白名单，支持CIDR格式IP段及域名统配符
* 支持TCP协议服务，也支持UDP协议
  * UDP采用UDP over TCP模式
* ......

## SG能解决什么问题？
* 无视内外网，安全访问内网资源的场景
* 需要P2P高带宽安全传输的场景
* 有公网IP，需要将内网服务发布出去的场景
* ......

## SG怎么使用？
* 下载APP并注册
* 下载合适的服务端版本，根据用户ID进行配置并运行
* 登录APP进行端口映射配置
* 使用配置的映射进行访问

## 有兴趣再细看

<details>
<summary>
	<mark><font size=3 color=darkred>查看详细</font></mark>
</summary>

# 
## 快速概览<a href=https://github.com/lazy-luo/smarGate/wiki/快速上手手册>【快速上手手册】</a> <a href="https://www.bilibili.com/video/BV1LM411k7Rf">【三方视频教学- B站】</a><br>
* 平台适配，支持linux、windows、macos、android（tob，小型机：hp-unix、solaris、AIX）<br>
* cpu架构，支持x86、arm、mips、riscv、LoongArch64（tob：alpha、PowerPC、SPRAC）<br>
* 注重安全，“内网”到“内网”的穿透，无需映射任何端口到外网，不更改任何防火墙配置<br>
* 注重带宽，”4G手机+v6宽带“采用P2P方式访问内网服务（基于TCP协议，v4支持NAT1-3穿透）<br>
* 注重节约，无需购买vps、无需公网IP；家中淘汰Android手机可做服务器<br>
* 注重可靠，随用随有，可7*24不间断服务，且不受UDP协议Qos之苦<br>
* 注重可控，客户端一点配置，且随时随地控制服务开启/关闭<br>
* 注重环保，免安装，体量小巧（mini版1MB左右） allinone，高性能且资源占用最少<br>
* 注重便携，无论工作或是度假，不管在任何地方，只要手机有网络，一切尽在掌控<br>
* ......如果这都是你想要的！请耐心继续往下看；如果你还想要...请提issue，【更新历史】也有看头哦<br>
* 免费，测试稳定后考虑开源. <br>
* 包含一个android客户端和需内网安装的服务端.<br>

## APP端配置（必须）--- 无法正常使用典型情况
* 必须配置“允许后台运行”权限，否则切后台即被系统断连
* 必须配置“休眠时始终保持网络连接”，否则一旦休眠则被系统断连
* 可以配置“允许自启动”权限，否则Android服务端模式下无法开机启动（v0.30及后续版本）
* 可以配置“麦克风”权限，否则Android服务端无法提供语音监听功能（v0.30及后续版本）
* 注意：SG官方代理不提供到港澳台及国外IP的数据转发
## smarGate是什么？<br>
#### 官方命名为“移动网关”，通过手机客户端将位于内网的服务端网络进行按需暴露，核心引擎采用c++实现。<br>
#### “移动网关”是用户私有网关，所有共享访问入口都在客户端，不是类似其它穿透工具主推的面向域名的公共访问入口。打个比方：smarGate是将防盗门随身携带，其它穿透产品是将防盗门放到公共场所，额...虽然需要钥匙，但有种职业叫开锁匠<br>

##### 具备如下技术特点：<br>
* 安全性 <br>
  * 手机客户端作为主要的访问入口，按需开放，及时关闭。<br>
  * 支持服务端间端口映射组网（v0.31及以后版本）。<br>
  * 电脑可以接入手机热点或wifi环境下通过访问手机开放的端口穿透到内网进行访问（客户端会显示手机ip）。<br>
  * 手机网络一般为私有网段别人无法访问。<br>
  * 用户间隔离。<br>
* 扩展性<br>
  * 基于内网网段代理，可以配合众多工具实现各种网络服务能力（telnet、ssh、http服务、内网摄像头、远程桌面等）<br>
  * 面向极客，可访问自定义的内网服务（rpc）<br>
* 便利性<br>
  * 手机客户端一点配置<br>
  * 服务能力动态增减<br>
* 高性能<br>
  * 0.1.1版本开始采用自主网络引擎，性能高，千元手机客户端能支持1千以上的并发共享访问<br>
  * 高性能设计：<br>
  	* 跨平台实现 socket 多路复用，支持：poll、epoll、kqueue、port、select、IOCP 等模型<br>
	* 采用 lock-free 算法<br>
	* 线程池设计<br>
	* socket 连接池<br>
	* 多级任务队列 <br>
	* ...<br>
<details>
<summary>
	<mark><font size=6 color=darkred>附：交互示意图</font></mark>
</summary>
<img src="https://github.com/lazy-luo/smarGate/blob/master/res/smarGateArch.png" /><br>
</details>
	
## smarGate有什么主要功能？<br>
* 支持代理穿透<br>
  * 官方提供免费的代理服务器（共享带宽，多人共用时比较慢，最佳实践为启用自有代理服务器）<br>
  * <I>如果自己有云服务器（具备公网ip），用户可自定义自己的代理服务器，且在代理服务器上安装proxy_server。所有数据传输走用户配置的代理服务器（代理服务器需要证书，可自动生成也可配置已有证书）</I> <br>

```  
  1、“代理服务器”配置如下（代理服务器必须允许任意端口“入站”连接）：
```
```
  <?xml version="1.0" encoding="GBK"?>
    <app-config code="PROXY" name="proxy-server">
        <app-parameter>
	        <proxy-service-port value="9001"/><!--自定义代理端口 -->
		<owner-id value="xxxx" /><!-- xxxx 为注册成功返回的用户ID -->
		<access-token value="nnnnn"/><!--访问token，必须为数字【可选配】 -->
		<ssl-create-certfile value="true" /><!-- 如未用如下选项指定证书，则自动生成证书【必须确保安装openssl】，默认为 false 代表无需自动生成 -->
          <!-- 如果自己有证书及私钥，则配置如下项，启动安全的SSL通道，其中文件名需要配置正确；没有证书则不需要配置，可启用上面自动生成证书选项
	        <ssl-cacert-file value="xxx.crt"/>
	        <ssl-privatekey-file value="xxx.key"/>
          -->
       </app-parameter>
       <moudle-parameter>
        <log-level value="LOG_ERROR"/>
        <log-write-mode value="CONSOLE_ONLY"/>
      </moudle-parameter>
  </app-config>
```
```
  2、"服务端"中增加如下配置：
```
```
......
    <app-parameter>
       	     <ssl-create-certfile value="true" />
       <!-- 如果代理服务器启动安全的SSL通道，这里必须配置证书及私钥
	     <ssl-cacert-file value="xxx.crt"/>
	     <ssl-privatekey-file value="xxx.key"/>
       -->
    </app-parameter>
    <moudle-parameter>
      ......
    </moudle-parameter>
    <!-- 配置上述代理服务器的ip或域名+端口，注意：ip必须为公网IP。ssl选项必须配置正确，如果代理服务器有证书（包括自动生成证书）且生效则配置为true否则为false -->
    <channel address="xxx.xxx.xxx.xxx:9001" ssl="true" token="nnnnn" /><!--访问token，必须与代理服务器一致，如果没有则不配 -->
```
* 支持p2p通道<br>
  * 使用TCP协议进行p2p穿透，提升安全性<br>
  * 不是所有的网络都支持p2p，取决于两端NAT类型
  * v0.14以上版本，直接支持ipv6，且能提供防火墙穿透
  * P2P测试结论：一端是NAT4，另一端是NAT3或NAT4时无法打通<br>
注：NAT1-〉Full Cone ， NAT2-〉Restricted Cone ， NAT3-〉Port Restricted Cone ， NAT4-〉Symmetric<br>
  <table>
	<th>服务端 NAT</th><th>客户端 NAT</th><th>P2P成功</th>
	<tr><td>NAT1-3</td><td>NAT1-3</td><td>YES</td></tr>
	<tr><td>NAT1-2</td><td>NAT4</td><td>YES</td></tr>
	<tr><td>NAT4</td><td>NAT1-2</td><td>YES</td></tr>
	<tr><td>NAT4</td><td>NAT3-4</td><td>NO</td></tr>
	<tr><td>NAT3-4</td><td>NAT4</td><td>NO</td></tr>
  </table>
  
* 支持外网发布（有违安全设计理念，v0.31版本开放）<br>
  * 其它内网穿透工具的主推模式，将内网服务直接映射到外网端口<br>
* 支持服务端之间的P2P端口映射（v0.31及以后版本） <br>
  * 具体配置主要通过 ip@index方式支持<br>
  
<details>
<summary>
	<mark><font size=6 color=darkred>附：主要功能简述</font></mark>
</summary>
	
```	
1、支持基于tcp的P2P连接隧道
	。安全可靠，避免Qos
2、支持所有基于tcp的各类协议”透明代理”
	。可代理所有内网tcp服务（ssh、rdp、smb、vnc、摄像头、数据库服务等）
3、支持HTTP、HTTPS to HTTP
	。支持http-head rewrite，支持将https服务代理成http
4、支持udp over tcp
	。支持udp协议的服务代理
5、透明方式（无需关注ipv6地址）支持ipv6隧道
	。自动建立v6隧道，访问时始终使用v4地址
6、支持自定义代理（需外网ip），接管所有数据转发
	。无法p2p时，自动连接自定义代理，实现数据转发
7、自定义代理支持token及白名单配置
	。支持安全机制
8、支持多级级联代理
	。支持链式代理，支持多级无环代理
9、支持手机作为访问唯一入口 —— 安全 + 移动便捷
	。手机在手、随用随有
10、端口映射全动态配置，支持映射配置“热拔插”
	。代理增、删及时生效，无需重启
11、所有功能app端“一点配置”
	。客户端一点配置，服务端运行时免配
12、支持P2P隧道及自定义代理隧道自动探测及连接
	。无需干预，app自动连接，自动重试
13、支持动态协商端口,支持指定协商端口
	。默认动态端口协商，支持配合防火墙配置协商端口
14、支持隧道连接优先级（P2P—>自定义代理-->官网代理）
	。数据传输时，支持优先级隧道
15、支持ssl加密隧道
	。支持P2P及代理隧道ssl加密，确保数据传输不泄密
16、支持流量限制
	。支持进行网络带宽限制，默认不限流
17、支持网络切换（如：移动<—>wifi）自动识别+自动连接
	。app端智能重连，始终确保服务可用性
18、支持不同局域网主机间端口映射 —— 如有一端主机有外网ip则可直接外网访问（version > v0.31）
	。支持服务端组网映射，流量无需通过手机app（传统穿透模式）
19、app支持服务端模式，可以将手机配置成服务端
	。android手机可作为服务端
20、支持远程文件管理功能：浏览、上传、下载、删除，支持断点续传（version >= v0.31.6）
	。在有p2p或自定义代理时，激活文件管理功能，可对手机和服务端电脑文件进行基本操作
21、支持内置socks5、http代理（version >= v0.32.1）
	。毕竟有三方专业工具如ss5、squid等，因此socks5及http代理是可选的功能
22、socks5、http代理支持域名和IP白名单（version >= v0.32.1）
	。域名白名单支持四种模式匹配(完全匹配、向前匹配、向后匹配、中间匹配)，默认配置文件名.white_list
	。IP白名单支持CIDR格式ip-range配置，默认配置文件名.ipchecks
。。。待续
	
```
</details>
	
## 使用指南:<br>
<a href="https://www.bilibili.com/video/BV1LM411k7Rf">三方视频教学- B站</a><br><br>
<a href="https://www.baidu.com/s?wd=smargate%20内网穿透">使用实践-度娘</a><br><br>
<a href="https://www.google.com/search?q=smargate+内网穿透">使用实践-google</a>
### 1、下载app && 注册新用户
* 下载android app（app-release.apk包含客户端和服务端）支持armv7及arm64 cpu架构<br>
* 注册新用户（邀请码必填，为数字，可任意填。ps：如果必填信息未填完整,或包含中文字符，会注册失败）<br>
* 注册成功后请务必记住返回的服务ID(N) 【重要】：注册成功后务必在1小时内完成首次登录<br>
<details>
<summary>
	<mark><font size=5 color=darkred>展开图示</font></mark>
</summary>
<img src="https://github.com/lazy-luo/smarGate/blob/master/res/login.png" /><br>
<img src="https://github.com/lazy-luo/smarGate/blob/master/res/reg.png" /><br>
</details>

### 2、下载服务端 && 配置
* 下载内网服务器适合的服务端版本（目前支持linux-x86-32/64，windows，及linux-arm【树莓派、群晖】,另：Android app自带服务端模式）<br>
* 解压服务端压缩包，修改配置文件(conf-proxy.xml):<br>
<details>	
<summary>
	<mark><font size=5 color=darkred>配置样例</font></mark>
</summary>
	
```
  <?xml version="1.0" encoding="GBK"?>
    <app-config code="PROXY" name="proxy-server">
       <app-parameter>
	<!-- [ none | first | only ] ,none is default. 为P2P连接启用SSL加密，only代表只接受加密连接 -->
	<ssl-tunnel-required value="first" />
	<!-- 如未用如下选项指定证书，则自动生成证书【必须确保安装openssl】，默认为 false 代表无需自动生成 -->
	<ssl-create-certfile value="true" /> 
 <!-- 以下选项仅适用dynamic下的mini版本，指定ssl库及crypto库实际文件，linux下可由：ldd $(which openssl)|grep -E "libssl|libcrypto"|awk '{print $1}' 获取
	<libssl value="libssl.so" />
	<libcrypto value="libcrypto.so" />
 -->
       </app-parameter>
       <moudle-parameter>
        <log-level value="LOG_ERROR"/>
        <log-write-mode value="CONSOLE_ONLY"/>
        <app-name value="xxxxx [name of service points]." /><!-- need modify -->
        <app-description value="yyyyy [description of service points]" /><!-- need modify -->
	<!-- user-audit need modify (N 为注册成功返回的服务ID，index为自定义的服务端实例序号，建议从1开始，不能重复. 例如:[12345:1])-->
        <user-audit value="N:index"/>
    </moudle-parameter>
  </app-config>
```
</details>

### 3、运行内网服务端(命令参数说明 i:最大接入连接数,o:最大接出连接数,w:最大线程数)<br>
* linux下执行命令：chmod +x proxy_server && nohup ./proxy_server -i1000 -o1000 -w8 >/dev/null & <br>
* windows下执行命令：proxy_server.exe -i1000 -o1000 -w8 <br>
* Android 手机/设备：运行app -〉编辑模式下，配置服务端信息 -〉打开“服务端”开关 -〉重启app <br>
* OpenWrt mips设备安装请见：<a href=https://github.com/lazy-luo/smarGate/issues/65>【MIPS linux下正确使用方式】</a><br>
### 4、登陆手机app && 配置端口映射 <a href="https://github.com/lazy-luo/smarGate/wiki/常用服务穿透配置">【常用服务配置】</a><br>
* 在客户端中可以看到上线的服务端（“访问点”），可以在客户端上定义端口映射规则<br>
<details>
<summary>
	<mark><font size=5 color=darkred>展开图示</font></mark>
</summary>
<img src="https://github.com/lazy-luo/smarGate/blob/master/res/proxy.png" /><br>
<b>服务端间端口映射配置需要在ip后加上服务端index序号，格式为：ip@idx</b>
<img src="https://github.com/lazy-luo/smarGate/blob/master/res/server-proxy.png" /><br>
</details>

### 5、电脑或手机可以直接访问手机客户端设置的服务（如ssh、http等）<br>

</details>

## 补充说明:<br>
* 所有版本已经打包了依赖，开箱即用.<br>
* 系统将自动清除30天以上未使用的“僵尸账号”.<br>
* Android 客户端需要权限:<br>
>> 1、后台执行权限（如果不允许，则app进入后台会断开连接）<br>
>> 2、网络访问权限（基本权限）<br>
* 手机设置 (Android):<br>
>> 1、设置 -> 无线及网络 -> WLAN -> 系统休眠保持连接  "允许" （否则，系统休眠会被断连）<br>
>> 2、设置 -> 无线及网络 -> 移动网络 -> 高级 ->始终保持数据连接 "允许"<br>

<details>
<summary>
	<mark><font size=5 color=darkred>常见问题答疑</font></mark>
</summary>
	
* Q：如何下载安装 android app？<br>
  >> 1、用android手机浏览器打开 https://github.com/lazy-luo/smarGate/raw/master/app-release.apk <br>
  >> 2、弹出框中下载安装 <br>
  >> 网盘链接为最新测试版本，github上版本稍有滞后 <br>
  >> 附网盘下载地址： https://pan.baidu.com/s/14Iq60kxHW711NVoCVKWySg <br>
  >> gitee地址（速度快些，不会有图片无法显示问题）：https://gitee.com/lazy-luo/smarGate <br>
  >> 如有需要请添加微信：ws_lzy008 注明：smarGate ，视情况组建技术讨论群<br>
* Q：需要访问家中局域网多台设备，是否每台都需要安装服务端？<br>
   >> A：不需要，只需选择任意一台设备安装服务端即可。<br>
* Q：为何有时连接不上？<br>
   >> A：服务端空闲约2-3分钟，会自动断开，须等待10秒左右重连。<br>
* Q：ipv6为何无法P2P？<br>
   >> A：请将客户端及服务端更新到最新版本；确保手机与内网电脑能获取到全局ipv6地址；确保没被防火墙拦截（windows）；排查两个ipv6是否能路由出去；查看hosts文件确保hostname能解析到ipv6地址。<br>
* Q：IPv4及IPv6的P2P连接为何没有UDP端口？<br>
   >> A：smarGate基于TCP协议进行P2P穿透，具备更好的安全性，及连接可靠性。<br>
* Q：手机NAS客户端为何无法登录？<br>
   >> A：确保手机NAS客户端ip黑名单中没有localhost（127.0.0.1）。<br>
* Q：如何将异地公司内网机器共享给多地团队？<br>
   >> A：手机连接wifi，让团队成员电脑连接手机IP：PORT，直接通过手机代理进行访问。实测，2k以上的手机，可以带上百人团队共享访问。<br>
* Q：为何windows服务端没有控制台黑框？<br>
   >> A：为了防止误操作关闭服务端，新版本windows服务端采用后台方式运行。如需关闭，请用“任务管理器”<br>
* Q：P2P时流量是否还需要走中间代理？<br>
   >> A：不需要，直接点对点连接，网速取决于你的客户端及服务端所在网络。<br>
* Q：smarGate后台运行是否很耗电？<br>
   >> A：经过长时间测试，按偶尔使用的频次，耗电量和任意一个系统进程相近，极低；频繁后台使用情况，长时间“后台”使用，整体耗电量等同于偶尔使用微信的耗电量。电源管理提示“后台频繁刷新。。。”，不用管它，后台传输数据都会有此提示，关键看耗电排名<br>
* Q：smarGate连接优先级规则？<br>
   >> A：首选P2P连接，无P2P时使用自定义代理连接，无前两者连接时使用官方代理连接。<br>
* Q: 同一个用户能否多处登录 ？<br>
   >> A: 可以多点登录，但同一时刻只能有一个客户端可以进行P2P；服务端单台机器只能启1个实例，服务端各实例配置确保序号不重复，否则将无法正常使用。<br>
* Q: 服务端能否支持Android手机 ？<br>
   >> A：v0.27版本Android app加入了“服务端模式”的支持。<br>
* Q: 客户端不同颜色表示啥意思？<br>
   >> A:ipv4下P2P标识为：<br>
   ![ipv4 p2p](https://github.com/lazy-luo/smarGate/blob/master/res/ipv4p2p.png)<br>
   >> A:ipv6下P2P标识为：<br>
   ![ipv6 p2p](https://github.com/lazy-luo/smarGate/blob/master/res/ipv6p2p.png)<br>
   >> A:自定义路由标识为：<br>
   ![userdefineproxyer p2p](https://github.com/lazy-luo/smarGate/blob/master/res/userdefineproxyer.png)<br>

</details>

## 最佳实践<br>  
* 以下为推荐使用的最佳实践，供参考：<br> 
  1、android客户端设置为“自动登录”，免除每次输入用户名/密码的麻烦;<br> 
  2、android客户端设置好后让其在后台运行，如果始终保持前台会定时刷新，webview控件空耗电，你懂的;<br>
  3、服务端始终保持后台运行，安全放心，只有你自己才能访问；<br>
  ...使用场景...<br>
  <a href="https://cloud.tencent.com/developer/article/1926888">【家用摄像头P2P直连】</a><br>
## 免责申明<br>  
* 请您仔细阅读以下申明，您在使用smarGate工具软件，表明您对以下内容的接受：<br> 
  1、严禁使用本软件从事计算机黑客以及其他任何危害计算机信息网络安全的行为;<br> 
  2、本软件属于正规网络接入软件，请合理，合法的使用；勿用于违反法律，道德及影响他人利益的活动；如果因用于非法用途，由此造成的不良后果，由用户自行负责，本软件开发者不承担任何责任及损失。<br>
## 捐助
如果您觉得 smarGate 对你有帮助，欢迎给予一定的捐助来维持项目的长期发展！<br>
ps：捐赠建议附上注册用户名<br>
<details>
<summary>
	<mark><font size=5 color=darkred>微信捐赠</font></mark>
</summary>
<img src="https://github.com/lazy-luo/smarGate/blob/master/res/donation.png"/>
</details>

## 附录<br>  
<details>
<summary>
	<mark><font size=5 color=darkred>更新历史</font></mark>
</summary>
	
### 2025-03-25<br>
1、文件管理新增空目录删除功能<br>
2、服务端间连接增加使用时连接功能（20秒内重连1次）<br>
3、增强稳定性，修复异常退出问题<br>

### 2024-10-12更新到v0.40.4：<br>
1、新增PROXY协议，单端口同时支持socks5及http代理<br>
2、新增http代理用户/密码认证<br>

```
<app-parameter>
	...
	<httpx-user value="user" />
	<httpx-passwd value="pwd" />
	<socks-user value="user" />
	<socks-passwd value="pwd" />
	...
</app-parameter>
```
3、其它优化<br>

### 2024-08-20<br>
1、提升文件传输速度<br>
2、其它优化<br>

### 2024-08-17<br>
1、修复网络出口变化时服务端长时间丢失的BUG<br>
2、改进P2P连接机制，提升P2P连接成功率<br>

### 2024-08-06更新到v0.40.3<br>
1、修复windows下代理连接偶发断开的BUG<br>
2、修复windows下低带宽时高CPU占用的BUG<br>
3、服务端支持动态资源回收，适合内存限制设备<br>
4、新增编译包，支持LoongArch64架构<br>
5、版本更新到v0.40.3<br>

### 2024-07-11<br>
1、修复代理地址错误显示为localhost的BUG<br>
2、修复windows下偶发coredump的BUG<br>

### 2024-05-11<br>
1、启用异步连接，防止慢连接阻塞正常连接<br>
2、修复链式代理、Socks5、http代理在特定情况下无法释放连接的BUG<br>

### 2024-04-27更新到v0.40.2：<br>
1、改进P2P的连接成功率<br>
2、修复部分已知BUG<br>
3、版本更新到v0.40.2<br>
  
### 2024-04-18：<br>
1、收藏夹BUG修复<br>
2、新增服务备注功能，便于服务识别及打标<br>
  
### 2024-04-10：<br>
1、VIP支持百度地图定位<br>
* APP服务端支持GPS定位
* 百度地图开放平台，自行申请“浏览器端”AK，然后将AK配置到SG客户端中，即可正常使用地图定位功能
  
2、版本更新到v0.40.1<br>

### 2024-02-02：<br>
1、APP易用性更新，后续版本将采用全新界面<br>
2、修复特定情况无法创建ipv6隧道的BUG<br>
3、APP增加收藏夹功能，常用连接一览无余<br>
4、版本更新到v0.32.3<br>

### 2023-11-28：<br>
1、老幼安全防护，支持GPS定位，便于掌握关怀对象所在经纬度（自行手动授权）<br>
* 此功能仅支持Android服务端<br>
* 坐标获取成功，则经纬度坐标将会自动复制到剪贴板<br>

2、其它优化<br>

### 2023-11-17更新到v0.32.2：<br>
1、socks协议支持用户名/密码验证<br>
2、支持保存及播放录音（VIP）<br>
3、版本更新到v0.32.2<br>

### 2023-10-25更新到v0.32.1：<br>
1、修复bug<br>
2、完善支持socks协议(仅支持ipv4 tcp)<br>
3、完善支持HTTP proxy协议<br>
4、APP支持VIP功能许可<br>
5、版本更新到v0.32.1<br>

### 2023-09-08更新到v0.31.12：<br>
1、修复bug<br>
2、试验性支持socks协议(仅支持ipv4 tcp)<br>
3、新增内置支持HTTP proxy协议<br>
4、内存回收（适用于内存限制设备）<br>
5、全异步方式提升响应速度 <br>
6、版本更新到v0.31.12<br>

### 2023-08-29更新到v0.31.11：<br>
1、文件管理支持默认按时间排序<br>
2、新增macos M1/M2支持<br>
3、版本更新到v0.31.11<br>

### 2023-06-03更新到v0.31.10：<br>
1、网络可靠性优化<br>
2、优化网络传输效率<br>
3、版本更新到v0.31.10<br>
	
### 2023-03-04更新到v0.31.9：<br>
1、APP服务端模式新增“无障碍”服务，用户自行打开,实现自动重启<br>
2、APP端操作优化：新增点击操作自动填充功能，便于新增配置<br>
3、修复mips路由器下安装自定义代理无法提供服务的BUG<br>
4、提供服务端自定义代理域名定时ip刷新功能（动态域名）<br>
5、其它优化<br>

### 2022-12-14更新到v0.31.8：<br>
1、APP服务端模式支持配置自定义代理及SSL加密<br>
2、自定义代理服务器支持SSL自签名证书下发<br>
3、其它优化<br>

### 2022-11-04更新到v0.31.7：<br>
1、提供一键版本升级功能，无需手动更新<br>
* 此功能版本源指向github，如无法更新，请确认github连通性<br>
* 更新后一般10-20秒左右恢复可用<br>
* 服务端提供自动更新选项（每天检测一次），默认关闭<br>	
```
<auto-update value="true" />
```

### 2022-10-20更新到v0.31.6：<br>
1、文件管理增加删除文件功能<br>
2、文件管理增加断点续传功能<br>
3、文件管理增加文件时间<br>
4、文件管理windows下增加切换磁盘操作<br>
* 此功能仅在有P2P连接或自定义代理连接时激活<br>
* 通过拖拽模式进行上传和下载<br>	
* 通过双击弹出文件删除确认框<br>		

### 2022-10-14更新到v0.31.5：<br>
1、修复自定义代理短间隔重连情况下连不上的BUG<br>
2、新增了简易文件上传下载功能，可方便同步异地文档<br>
* 此功能仅在有P2P连接或自定义代理连接时激活<br>
* 通过拖拽模式进行上传和下载<br>	
	
3、版本更新到v0.31.5<br>
	
### 2022-09-05：<br>
1、解决自定义代理连接异常断开BUG<br>
2、版本保持不变<br>

### 2022-08-30更新到v0.31.4：<br>
1、降低运行时虚拟内存占用<br>
2、常规性优化<br>
3、版本更新到v0.31.4<br>

### 2022-08-14更新到v0.31.3：<br>
1、修复mips架构系统无法连接自定义代理的BUG<br>
2、修复HTTP协议加载完成时间长的问题<br>
3、版本更新到v0.31.3<br>

### 2022-08-06更新到v0.31.2：<br>
1、修复Windows平台偶发闪退BUG，增强稳定性<br>
2、P2P连接及自定义代理进行keep-alive操作，尽可能避免重连时间窗口，提升可用性<br>
3、其它可用性优化,降低app能耗<br>
4、版本更新到v0.31.2<br>

### 2022-07-28更新到v0.31.1：<br>
1、修复特定情况下，服务端重启，组网配置不生效的BUG<br>
2、修复NAT1服务器P2P协商BUG<br>
3、版本更新到v0.31.1<br>

### 2022-07-22更新到v0.31: <br>
1、提供服务端之间端口映射，服务端如有公网ip则可直接从公网访问(仅需在app上配置)
* 配置方式，在原有映射配置“远程ip”配置中支持：ip@idx方式进行配置(idx为不同“访问点”的序号)
* 此种方式配置的“本地端口”实际是在当前“访问点”所在主机上（注意：不在APP所在手机上）
* 服务端间如能P2P成功（或自定义代理连接成功）则配置的映射将生效，否则不生效
* APP上只有在P2P连接时才会定时刷新服务端间代理状态
* 配置成功后需要等待10秒左右才能在App上看到实际状态

2、版本升级到v0.31<br>

### 2022-06-30: <br>
1、修复32位大端机器运行服务端，无法正常代理的BUG<br>
2、版本暂保持不变<br>

### 2022-05-17: <br>
1、服务端支持自动生成自签名证书（默认文件名为server.xxx）<br>
-->a、配置ssl-create-certfile选项 <br>
```
<app-parameter>	
  <ssl-create-certfile value="true" />
...
</app-parameter>
```
-->b、确保安装openssl <br>
-->c、不要指定证书文件（不配置 ssl-cacert-file 及 ssl-privatekey-file）<br>
	
### 2022-05-04: <br>
1、支持riscv32/64架构，编译时同mips架构使用musl库进行链接<br>
2、优化网络传输层<br>
3、版本暂保持不变<br>
	
### 2022-02-07更新到v0.30.4: <br>
1、提供mips64el支持<br>
2、增加app端系统图标显示 <br>
3、其它优化<br>
	
### 2021-11-06更新到v0.30.3: <br>
1、修复app端内存占用只显示jvm不包含native的BUG<br>
2、优化网络引擎，提升高并发下的稳定性及公平性 <br>
	
### 2021-10-17更新到v0.30.2: <br>
1、自定义代理支持ssl验证<br>
2、网络P2P情况下，支持配置成ssl隧道（ **要求服务端必须配置证书** ）<br>
```
<app-parameter>
  <ssl-tunnel-required value="first" /><!-- 取值有3个：none、first、only -->
  ...
</app-parameter>
```
3、其他优化<br>
	
### 2021-09-24更新到v0.30: <br>
1、提供了Android服务端开机自启动支持(仅服务端模式，且需要自行手动授权)<br>
2、网络P2P情况下，Android服务端支持实时音频（麦克风权限需要自行手动授权，必须打开SG界面才能录音）<br>
3、其他优化<br>

### 2021-05-03更新到v0.29.2: <br>
1、修复Android高版本无法退出问题<br>
2、优化网络:修复了可能带来网络延迟的BUG，进一步提升网络传输速度<br>
3、提供版本号展示，便于客户端及服务端版本管理<br>
4、优化app cpu占用，降低能耗<br>

### 2021-03-05更新到v0.29: <br>
1、修复ipv6与ipv4网络切换存在的服务端core-dump问题<br>
2、客户端新增ipv4-only网络模式选项，用于在ipv6网络环境下由于特殊需求需要使用ipv4进行p2p连接的场景（强制使用ipv4进行网络穿透）<br>
3、其它一些bug修复<br>
注意：特定场景下由于存在core-dump的致命问题，0.29版本需要同时更新客户端及服务端
	
### 2020-12-13更新到v0.28: <br>
1、自定义代理增加token支持，防止非法访问。同时支持配置访问许可列表(access-token只能输入数字,access-restricting可输入允许的SID，多个SID用“:”分隔,access-restricting可不配) <br>
 A、代理服务器配置：
 ```
 <app-parameter>
  <proxy-service-port value="9001"/>
  <access-token value="nnnnn”"/>
  <access-restricting value="xxxxx"/>
  …
 </app-parameter>
 ```
 B、服务端配置(token必须与代理服务器一致):
 ```
 <channel address="x.x.x.x:9001" ssl="true" token="nnnnn" />
```
2、对于隧道超时断开机制做了优化（仅针对P2P隧道及用户代理隧道）：只要有连接接入且连接正常情况下客户端会随机时延发送心跳，尽量防止超时断开。 <br>
 场景：ssh访问时，较长时间不输入会保持心跳，不至于1两分钟空闲就断开了。

### 2020-05-23更新到v0.27：<br>
1、去掉root权限获取功能，保持最低权限要求。暂不开发支持配置1024以下端口的能力<br>
2、由于自用树莓派被孩子摔坏了，只能压榨淘汰手机剩余价值，Android app端增加“服务端模式”支持，可以放在家中作为服务器<br>

### 2020-04-30更新到v0.26：<br>
1、修复IP切换时配置的HTTP服务可能不可用的问题<br>
~~2、对已root手机，尝试获取root权限，支持配置1024以下的保留端口~~<br>
3、解决绝对路径执行（多为开机启动脚本）且不指定-f参数时无法定位默认配置文件问题<br>
4、服务端增加HTTP基于内容替换选项（影响效率，忽略压缩数据。对于部分js中将ip端口返回到浏览器的不规范内网web应用），默认不过滤内容<br>
```
	……
	<moudle-parameter>
		<http-content-type-filter value="application/javascript" />
		……
	<moudle-parameter/>
	……
```
5、服务端增加指定P2P协商端口选项，默认选择随机端口<br>
```
	……
	<moudle-parameter>
		<negotiation-port value="xxxxx" />
		……
	<moudle-parameter/>
	……
```
6、增加“官方代理”开关，默认打开。关闭时在任何情况下都不会走官方代理转发数据<br>
### 2020-03-13：<br>
1、修复tcp-cork特定条件下丢失writable-event造成网络延迟的BUG<br>
2、提升内存池运行性能<br>
3、增加 -f 命令行参数，可指定配置文件全路径<br>
4、其它优化，版本保持不变<br>
### 2020-01-18更新到v0.25：<br>
1、修复 http代理失效 BUG<br>
2、app端提供ipv6地址显示<br>
3、版本更新到0.25<br>
### 2019-11-30更新到v0.24：<br>
1、花生壳支持UDP了？好吧，支持一下UDP端口转发，游戏串流的朋友可以试用一下<br>
2、支持 UDP over TCP 模式<br>
3、其它小的优化<br>
### 2019-11-03：<br>
1、修复 memory leak BUG<br>
2、其它小优化，版本保持不变<br>
3、提升P2P重连可靠性<br>
### 2019-09-30更新到v0.23：<br>
1、修复弱网络环境下windows服务端高CPU占用BUG<br>
2、整体提升网络传输速度<br>
### 2019-09-20更新到v0.22：<br>
1、提升P2P检测可靠性<br>
2、修复windows下特定情况无法进行P2P连接的BUG<br>
3、客户端提供了手动p2p重连功能（弱网络环境下自动重连可能失败，此时可以手动重连）
### 2019-09-15：<br>
1、进一步降低在低速率下服务端cpu占用率<br>
2、常规优化，版本保持不变<br>
### 2019-09-10更新到v0.21：<br>
1、优化网络性能<br>
2、客户端支持显示实时网速<br>
### 2019-09-05：<br>
1、解决客户端修改密码后自动登录失败的BUG<br>
2、提供自动登录超时控制<br>
### 2019-09-01更新到v0.20：<br>
1、优化连接检查性能（提供并行异步检测）<br>
2、支持将HTTPS代理到HTTP（客户端http访问，服务端为https）<br>
### 2019-08-18更新到v0.19：<br>
1、性能优化<br>
2、解决特定条件下(自定义路由)无法可靠断开服务端连接的BUG<br>
3、进行静态编译，不再依赖inux系统gcc动态库，可直接在alpine中运行（需要创建软连接）<br>
4、支持编译为mini版本，不再静态编译openssl；对openssl库从0.9.8~1.1.1的全系动态兼容，二进制包缩小为1M左右（已放入dynamic目录，需配置ssl库）<br>
### 2019-05-27更新到v0.18：<br>
1、性能优化<br>
2、提供ipv6 P2P开关机制：&lt;ipv4-tunnel-first value="false"/&gt; 如需关闭ipv6点对点则设置为“true”，默认值为“false”<br>
3、增加客户端ipv6标志及连接状态提示<br>
### 2019-05-21：<br>
1、修复Raspbian jessie下无法检测IPv6的BUG<br>
### 2019-05-16更新到v0.17：<br>
1、性能优化<br>
2、提供P2P断开重连机制<br>
### 2019-05-04：<br>
1、修复服务端在挂载私有路由时当线程数量<4时偶发CPU高占用的BUG，版本保持不变<br>
### 2019-04-23更新到v0.16：<br>
1、修复服务端在挂载私有路由时偶发core dump的BUG<br>
### 2019-04-16更新到v0.15：<br>
1、修复IPV4/IPV6网络切换，无法P2P的BUG<br>
### 2019-04-15更新到v0.14：<br>
1、解决网络切换重连失败问题<br>
2、引擎性能优化<br>
3、新增对IPv6防火墙穿透支持（移动端支持ipv6，且内网服务端支持ipv6）<br>
【重要提示】v0.14版本将于之前版本不兼容，请务必更新版本！！！<br>
### ....初始版本v0.13<br>
</details>
