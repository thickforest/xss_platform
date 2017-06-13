原文: https://bbs.ichunqiu.com/thread-13187-1-1.html

本次整个项目所在目录: /var/www/html/XSS/

(1) 修改 config.php ,mysql数据库用户名密码

(2) 导入xssplatform.sql,执行
UPDATE oc_module SET code=REPLACE(code,'http://xsser.me','http://你的域名/XSS’);

(3) 修改config.php 注册改为normal,自己先免邀请码注册一个

执行
UPDATE `xss`.`oc_user` SET `adminLevel` = '1' WHERE `oc_user`.`id` =1 LIMIT 1;
升级为管理员

别忘了再改回 invite

(4) 修改 /etc/apache2/apache2.conf

<Directory /var/www/>
        Options FollowSymLinks
        AllowOverride All	# 如果是None,则.htaccess 无效
        Require all granted
</Directory>

确认 apache2 加载 rewrite模块

确认.htaccess 的 /XSS/index.php 路径是否匹配

(5) 短信提醒功能

修改 source/api.php 移动飞信帐号
