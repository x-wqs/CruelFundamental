## Get请求，向数据库发送获取数据的请求，从而获取信息。

1.1不做修、改、增数据，不影响资源的内容，无论进行多少次，结果都一样。

1.2Get请求是1024个字节。是整个URL的长度，不仅仅是参数值数据长度。

1.Get请求参数实在请求头中的，不安全。  login?username="babilong"&password="123456"

 

## 二、Post请求，同Get请求类似，都是向服务端发送数据，会创建新的内容。

2.1Post请求参数在请求体内，比较安全。

2.2Post请求不限制长度。

 

## 三、Put请求时向服务器发送数据，从而改变信息。 例 update

 

## 四、Delete请求，删除某一资源。

***总结：***

Get请求是向服务器发送获取数据的一种请求。

Post是向服务器提交数据的一种请求，在表单中，Method默认为get。

实质上，post和get只是发送机制不同并不是一个取 ，一个发。

Get方法需要Request.QueryString来获取变量的值，Post方法需Request.Form来获取

Put是幂等的