	wget --no-check-certificate https://raw.githubusercontent.com/clangcn/onekey-install-shell/master/frps/install-frps.sh -O ./install-frps.sh
	 chmod 700 ./install-frps.sh
	./install-frps.sh install

	------------------------------------
	./install-frps.sh config	修改配置
	./install-frps.sh update	更新
	./install-frps.sh uninstall	卸载
	frps -V				版本号
	------------------------------------

##安装过程：
###1. 选择下载网址：
2. 
	Please select frps download url:
	[1].aliyun (default)
	[2].github
	Enter your choice (1, 2 or exit. default [aliyun]): 
	---------------------------------------
	Your select: aliyun
	---------------------------------------


2.选择配置：

	Please input your server setting:

	Please input frps bind_port [1-65535](Default Server Port: 5443):7000
	frps bind_port: 7000
	#输入 frp 提供服务的端口，用于服务器端和客户端通信

	Please input frps vhost_http_port [1-65535] (Default vhost_http_port: 80):80
	frps vhost_http_port: 80
	#输入 frp 进行 http 穿透的 http 服务端口
	
	Please input frps vhost_https_port [1-65535] (Default vhost_https_port: 443):443
	frps vhost_https_port: 443
	#输入 frp 进行 https 穿透的 https 服务端口
	
	Please input frps dashboard_port [1-65535] (Default dashboard_port: 6443):
	frps dashboard_port: 6443
	#输入 frp 的控制台服务端口，用于查看 frp 工作状态
	
	Please input dashboard_user (Default: admin):
	frps dashboard_user: admin
	
	Please input dashboard_pwd (Default: 5MuI6puV):12345678
	frps dashboard_pwd: 12345678
	
	Please input token (Default: 2PyxSCK1Mv1GK6i6):
	frps token: 2PyxSCK1Mv1GK6i6
	#输入 frp 服务器和客户端通信的密码，默认是随机生成的
	
	Please input frps max_pool_count [1-200]
	(Default max_pool_count: 50):
	frps max_pool_count: 50
	 #设置每个代理可以创建的连接池上限，默认 50
	##### Please select log_level #####
	1: info (default)
	2: warn
	3: error
	4: debug
	#####################################################
	Enter your choice (1, 2, 3, 4 or exit. default [1]): 
	log_level: info
	#设置日志等级，4 个选项，默认是 info
	
	Please input frps log_max_days [1-30]
	(Default log_max_days: 3 day):
	frps log_max_days: 3
	#设置日志保留天数，范围是 1 到 30 天，默认保留 3 天
	
	##### Please select log_file #####
	1: enable (default)
	2: disable
	#####################################################
	Enter your choice (1, 2 or exit. default [1]): 
	log_file: enable
	#设置是否开启日志记录，默认开启，开启后日志等级及保留天数生效，否则等级和保留天数无效
	
	##### Please select tcp_mux #####
	1: enable (default)
	2: disable
	#####################################################
	Enter your choice (1, 2 or exit. default [1]): 
	tcp_mux: true
	
	##### Please select kcp support #####
	1: enable (default)
	2: disable
	#####################################################
	Enter your choice (1, 2 or exit. default [1]): 
	kcp support: true
	#开启Kcp通道
	
	============== Check your input ==============
	You Server IP      : 100.100.100.100
	Bind port          : 7000
	kcp support        : true
	vhost http port    : 80
	vhost https port   : 443
	Dashboard port     : 6443
	Dashboard user     : admin
	Dashboard password : 12345678
	token              : 2PyxSCK1Mv1GK6i6
	tcp_mux            : true
	Max Pool count     : 50
	Log level          : info
	Log max days       : 3
	Log file           : enable
	==============================================
	
	Press any key to start...or Press Ctrl+c to cancel
	frps install path:/usr/local/frps
	config file for frps ... done
	download frps ... done
	download /etc/init.d/frps... done
	setting frps boot... done
	
	
	3.确认之后，自动安装：
	+--------------------------------------------------+
	|        Manager for Frps, Written by Clang        |
	+--------------------------------------------------+
	| Intro: http://koolshare.cn/thread-65379-1-1.html |
	+--------------------------------------------------+
	
	Starting Frps(0.20.0)... done
	Frps (pid 25806)is running.
	
	+---------------------------------------------------------+
	|        frps for Linux Server, Written by Clang          |
	+---------------------------------------------------------+
	|     A tool to auto-compile & install frps on Linux      |
	+---------------------------------------------------------+
	|    Intro: http://koolshare.cn/thread-65379-1-1.html     |
	+---------------------------------------------------------+
	
	
	Congratulations, frps install completed!
	==============================================
	You Server IP      : 100.100.100.100
	Bind port          : 7000
	KCP support        : true
	vhost http port    : 80
	vhost https port   : 443
	Dashboard port     : 6443
	token              : 2PyxSCK1Mv1GK6i6
	tcp_mux            : true
	Max Pool count     : 50
	Log level          : info
	Log max days       : 3
	Log file           : enable
	==============================================
	frps Dashboard     : http://100.100.100.100:6443/
	Dashboard user     : admin
	Dashboard password : 12345678
	==============================================
#####安装结束打开 http://100.100.100.100:6443/ 进行端口配置

##4.FRPS 管理相关命令：
	frps status manage : frps {start|stop|restart|status|config|version}
###如:
	start: frps start
	stop: frps stop
	restart: frps restart

##5.到 DNS 网站去设置域名的绑定，直接 A 记录到服务器 IP 就好了，如：

	类型	主机记录		记录值
	A		nas	   100.100.100.100
	A		router	100.100.100.100

##Nas端口配置
	协议类型	代理名称	域名配置	内网主机ip	内网端口	远程主机端口	加密 	压缩
	tcp		nas1				192.168.1.100	5001	443		是	是
	tcp		drive				192.168.1.100	6690	6690	是	是
	tcp		photo				192.168.1.100	80		80	是	是
	tcp		note				192.168.1.100	5000	5000	是	是
	tcp		download			192.168.1.100	8000	8000	是	是
	tcp		audio				192.168.1.100	8800	8800	是	是
	tcp		video				192.168.1.100	9007	9007	是	是
	https	nas		nas.yourname.com	192.168.1.100	5001	443	是	是
	https	router	router.yourname.com	192.168.1.1	8443	443	是	是