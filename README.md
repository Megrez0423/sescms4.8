# Seecms
# sql注入漏洞

### BUG_Author: Megrez

### Affected version: Seecms

### Vendor: https://www.sem-cms.com/

### Software: https://www.sem-cms.com/TradeCmsdown/php/semcms_php_4.8.zip

![image](https://github.com/user-attachments/assets/b989312d-f06c-416e-83b5-04b2d98e12a9)


### Vulnerability File:

/xcR45q_Admin/SEMCMS_SeoAndTag.php

### Description:

seecms系统v4.8存在SQL注入漏洞在SEMCMS_SeoAndTag.php页面。
 参数lgid没有被正确处理。黑客可以利用这个漏洞来操纵系统的管理员账户，并可以完全控制其他账户的信息。
 状态：严重

漏洞代码：
elseif ($type == "edit") {

$row = mysqli_fetch_array($db_conn->query("SELECT * FROM sc_user WHERE ID=" . $_GET["ID"]));

The system seecmsv4.8 is vulnerable to SQL Injection via /xcR45q_Admin/SEMCMS_SeoAndTag.php.
 The parameter `id` is not sanitized correctly. The malicious actor can use this  vulnerability to manipulate the administrator account of the systemand  can take full control of the information about the other accounts.
 Status: CRITICAL

GET parameter ‘id’ exists SQL injection vulnerability

漏洞复现：

访问http://url/xcR45q_Admin/SEMCMS_User.php 获取ID参数

<img width="416" alt="image" src="https://github.com/user-attachments/assets/8ee10d59-1a34-4cde-9696-fa3af72e9090">
<img width="416" alt="image" src="https://github.com/user-attachments/assets/3e8d2917-775f-4caf-a299-aadd41e37acd">



Bp抓包之后 将payload插入 由于新建站点的时候数据库名的长度为5 所以payload构造为
-1%20or%20length(database())%20REGEXP%20char(94,53,36)
（判断数据库名长度是否为5）

插入payload查看回显 

<img width="416" alt="image" src="https://github.com/user-attachments/assets/5015a113-1275-46ea-838a-51d2e67d1642">

此时更改payload
-1%20or%20length(database())%20REGEXP%20char(94,54,36)
（判断数据库名长度是否为6） 
插入payload查看回显 

<img width="416" alt="image" src="https://github.com/user-attachments/assets/71739530-6151-45cd-abba-54808d6d12f5">

