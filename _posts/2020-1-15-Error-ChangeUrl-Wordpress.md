---
layout:     post                    # 使用的布局（不需要改）
title:      WordPress地址(URL)，不能随便更改！  # 标题 
subtitle:   URL in wordpress can't be changed #副标题
date:       2020-01-15              # 时间
author:     ZK                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:
  - 个人网站                               #标签


---

## WordPress地址(URL)，不能随便更改！

1.错误操作
  在后台的设置里，WordPress地址（URL）是不能随便更改的，只有站点地址（URL）可以随意动。如果更改了WordPress地址（URL），主页面可能就丢失了。

2.解决方法
以下操作在服务器终端执行  

1.输入一下指令，打开数据库。（要求输入的是数据库的密码）  
` mysql -u root -p `		  
2.选中之前创建的数据库，默认为wordpress  
`USE wordpress;`  
3.更改显示的列表中的option_values值,your_wordpress_url为正确的WordPress地址（URL）  
`UPDATE wp_options SET option_value="your_wordpress_url" WHERE option_name="siteurl";`    

## 然后就可以愉快地继续访问主页啦！





