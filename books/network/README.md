<!-- * [XSS跨站脚本攻击](/books/network/XSS.md)

* [SCRF跨站追踪攻击](/books/network/CSRF.md)

* [SQL注入攻击](/books/network/SQL.md) -->
# 常见的网络攻击方式

- [XSS跨站脚本攻击](#XSS)
- [CSRF跨站追踪攻击](#CSRF)
- [SQL注入](#SQL)


<a id='XSS'>XSS跨站脚本攻击</a>

1. 什么是XSS

    跨站脚本攻击指的是攻击者往web页面里插入恶意的html标签或javascript标签。
2. 举个例子

    （1）攻击者在页面中放了一个看似安全的链接`<a href='javascript:console.log(document.cookie);'>链接</a>`这样成功的读取cookie并可以将其发送至对应的服务器。
    （2）或者在论坛中国呢，添加评论时web端没有进行对应的防护，攻击者插入对应的表单并且成功了，这样用户将会将信息发送至攻击者的服务器

3. 防护

    （1）服务端设置httpOnly,这样客户端脚本将无法读取客户端的cookie
    （2）用户输入的地方，对标签进行过滤
    （3）配合token使用

<a id='CSRF'>CSRF跨站追踪攻击</a>

csrf是代替用户完成指定的操作，需要知道客户端页面的代码。而XSS是获取用户的数据，不需要知道页面代码和数据包

csrf跨站伪造请求，就是攻击者使用你的身份去发送恶意的请求，从而可以利用你的账号购买商品、发送邮件等。

主要是：

用户在登陆a网站后，浏览器返回并在本地存储cookie；
用户在网站a看到了不安全的网站b链接。这个链接指向一个含有iframe的标签，并且发送了http请求给网站a的服务端，因此会携带cookie这是服务端将会认为是网站a的用户发送了请求。

简单级别的攻击

我在网站a发布了一篇文章，并且文章的img是隐藏的并且src指向，网站a的服务器地址，并且携带query参数，这时将发送http请求。

高级的csrf攻击

在网站a中插入一个链接这个链接是指向攻击者网站的一个页面，这个页面添加了iframe,
这个iframe发送了http请求到a网站的服务器这个时候服务器接收到了请求验证后确定是用户攻击成功

防范:
通过增加token验证唯一用户，
或者验证码
内容加密

<a id='SQL'>SQL注入</a>

    sql注入主要是后端防护
    用户在提交表单的时候，输入sql语句，如果后端使用的是sql拼接的方式将会对数据库造成威胁



