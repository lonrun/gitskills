===============================
@2020年9月5日

1. Linux-把任务放到后台
	nohup .. &
	ctrl+z 配合 bg %jobnumber 使用
	jobs
	fg ##后台，调至前台执行
	bg ##后台，继续执行
	

=================
@2020年9月2日
1. tcpdump命令抓pppoe数据：
	tcpdump -X -s 0 -i eth1 pppoes 【http://itindex.net/detail/37157-linux-%E7%BD%91%E7%BB%9C-%E5%91%BD%E4%BB%A4】
	参考：man tcpdump 

2. 命令行动态显示文件内容
	tail -f -n 10 /var/log/pppd.log
	tail -f -n 10 /var/log/pppd.log |grep "Connect:" -A10
	参考：https://blog.csdn.net/weixin_41796956/article/details/104557770

=================
@2020年8月26日
1. 测试程序到tftp服务器根目录：
	cp cyz_1.4_mipsel_24kc.ipk ./image/


2. iconv_open失败，errno为22： invalid argument
	https://blog.csdn.net/violet089/article/details/51568667

	之前已经编译了openwrt的iconv版本：
	
	find / -name preloadable_libiconv.so

	cp /preloadable_libiconv.so /home/test/mesh/image/
	
	并下载到目标板 /lib，目标板执行：
		export LD_PRELOAD=/lib/preloadable_libiconv.so
		
=================
@2020年8月25日

1. find . -name 100-strip_charsets.patch -exec mv {} {}.bak \; 


=================
@2020年8月18 & 19日

1. 固件升级：


tftp更新：
	a).服务端tftp服务的安装参看：
		https://www.cnblogs.com/linfeng-learning/p/9284402.html
		////
		本人设置的tftp根目录为 /var/lib/tftproot.

	b).开发板的tftp更新
		【前置条件】开发板可以ping通tftp服务端
		把更新的文件（如 upgrade.bin）放至服务器tftp服务的根目录下，
		开发板执行 safeupgrade up 192.168.0.153:upgrade.bin 即可升级
	c). tfpt命令
		tftp -r

web更新：
	登录路由管理界面进行手动升级。

2. 安装软件包：
	使用tftp【scp端口未开放，且目标板也未包含该命令】可以从开发机传输软件包(*.ipk)至目标板进行运行测试。

	tftp方式：
	<<<<<<<<<<<<<<<<<<<<<<<<
	tftp -g -r cyz_1.0_mipsel_24kc.ipk 192.168.0.153
	opkg install cyz_1.0_mipsel_24kc.ipk 


3. 软件包版本的更新升级测试
	需要在Makefile文件中定义好软件包版本：
		如果更新了代码版本，但是在Makefile未同步更新软件版本
		目标板执行okpg install并未升级程序（是根据版本检查更新的！！）
		


=================
@2020年8月17日

find 使用案例详解：
	https://www.cnblogs.com/kelelipeng/p/11310023.html
	
	简单教程：https://www.runoob.com/linux/linux-vim.html	

	简单使用：
		find ./ -name Makefile |xargs grep "+libnl"


Vim 使用详解：
	https://www.cnblogs.com/libaoliang/articles/6961676.html
	https://www.cnblogs.com/eyong/p/3588646.html 【跳转至函数定义处等】 
	https://www.cnblogs.com/kinwing/p/11093900.html

