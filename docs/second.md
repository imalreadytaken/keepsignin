# 2018-06-08

#Laravel 环境配置

## 安装PHP
[http://php.net/downloads.php](http://php.net/downloads.php "PHP下载地址")
	
	后台运行脚本
	@echo off 
	if "%1"=="h" goto begin 
	start mshta vbscript:createobject("wscript.shell").run("""%~nx0"" h",0)(window.close)&&exit 
	:begin
	php-cgi.exe -b 127.0.0.1:9000 -c C:\pl\php\php.ini
	pause

## 安装MySql
Mysql注册为服务 mysqld --install

## 安装nginx
[http://nginx.org/en/download.html](http://nginx.org/en/download.html "nginx下载地址")

	# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000  
	#location ~ \.php$ {  
	#    root           html;  
	#    fastcgi_pass   127.0.0.1:9000;  
	#    fastcgi_index  index.php;  
	#    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;  
	#    include        fastcgi_params;  
	#} 
更改/scripts为$document_root
location语法规则：

	语法规则： location [=|~|~*|^~] /uri/ { … }
	= 开头表示精确匹配
	^~ 开头表示uri以某个常规字符串开头，理解为匹配 url路径即可。nginx不对url做编码，因此请求为/static/20%/aa，可以被规则^~ /static/ /aa匹配到（注意是空格）。
	~ 开头表示区分大小写的正则匹配
	~*  开头表示不区分大小写的正则匹配
	!~和!~*分别为区分大小写不匹配及不区分大小写不匹配 的正则
	/ 通用匹配，任何请求都会匹配到。
	多个location配置的情况下匹配顺序为（参考资料而来，还未实际验证，试试就知道了，不必拘泥，仅供参考）：
	首先匹配 =，其次匹配^~, 其次是按文件中顺序的正则匹配，最后是交给 / 通用匹配。当有匹配成功时候，停止匹配，按当前匹配规则处理请求。

在location / 中增加

	try_files $uri $uri/ /index.php?$query_string;

## 安装composer
https://getcomposer.org/download/](https://getcomposer.org/download/ "composer下载地址")
## 安装laravel
* 安装laravel：composer global require "laravel/installer"