## 自定义微信菜单

使用以下连接获得微信访问token

[https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&amp;appid=wx71299d053bdec038&amp;secret=7fb70420e6425c1cf45dc5353cbb5e16](https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=wx71299d053bdec038&secret=7fb70420e6425c1cf45dc5353cbb5e16)

使用以下链接

[https://api.weixin.qq.com/cgi-bin/menu/create?access_token=v1mga6woH8XMqxNZS_fD7BHOx4ayKrEEUacDZhHAc1jLqRx3t_BxZynHUNeCSWyxkbaRgKb5oaiRffjOKcwVzDoEXfx7EyMyzR7cLgq4c_L92RfTX4Xw4T_3K_V_EYDoCJFaADAVCY](https://api.weixin.qq.com/cgi-bin/menu/create?access_token=v1mga6woH8XMqxNZS_fD7BHOx4ayKrEEUacDZhHAc1jLqRx3t_BxZynHUNeCSWyxkbaRgKb5oaiRffjOKcwVzDoEXfx7EyMyzR7cLgq4c_L92RfTX4Xw4T_3K_V_EYDoCJFaADAVCY)

设置菜单

Body内容为：

{

&quot;button&quot;:[

{

&quot;name&quot;:&quot;微主页&quot;,

&quot;type&quot;:&quot;view&quot;,

&quot;url&quot;:&quot;http://jdkj99999.com/gotomainpage?dest=sjgl&quot;

},

{

&quot;name&quot;:&quot;组织活动&quot;,

&quot;sub_button&quot;:[

{

&quot;type&quot;:&quot;view&quot;,

&quot;name&quot;:&quot;我的活动&quot;,

&quot;url&quot;:&quot;http://www.sohu.com&quot;

},

{

&quot;type&quot;:&quot;view&quot;,

&quot;name&quot;:&quot;我的会议&quot;,

&quot;url&quot;:&quot;http://www.163.com&quot;

},

{

&quot;type&quot;:&quot;view&quot;,

&quot;name&quot;:&quot;在线学习&quot;,

&quot;url&quot;:&quot;http://www.126.com&quot;

}]

},

{

&quot;name&quot;:&quot;常见问题&quot;,

&quot;sub_button&quot;:[

{

&quot;type&quot;:&quot;view&quot;,

&quot;name&quot;:&quot;历史消息&quot;,

&quot;url&quot;:&quot;http://www.sohu.com&quot;

},

{

&quot;type&quot;:&quot;view&quot;,

&quot;name&quot;:&quot;提点意见&quot;,

&quot;url&quot;:&quot;http://www.163.com&quot;

},

{ &quot;type&quot;:&quot;view&quot;,

&quot;name&quot;:&quot;关于我们&quot;,

&quot;url&quot;:&quot;http://www.sina.com&quot;

}]

}]

}