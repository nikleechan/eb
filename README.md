# eb
说明：这个教程属于我复制hangaj的，他可能也是复制于其他人。
复制这个教程的原因是我安装的时候，代码里面的链接已经失效，所以我复制一遍方便修改代码。
如有侵权请联系我删除。

同时，结合时光轴教程进一步整合了证书申请内容。



### embyonekey

- 群辉emby套件版服务端一点五键白嫖
- 左点点右点点,算你一点五键吧

# 提前说下
啥也不会瞎捣鼓的
<br/>所以~~~
<br/>请保证在未在Web Station中新建任何虚拟主机
<br/>请按照说明路径正确设置
<br/>出啥问题我也不负责
<br/>看不到图片或者脚本无法下载运行的
<br/>请科学好raw.githubusercontent.com网址

### 步骤说明
<br/>0. 在群辉中安装好Web Station跟EMBY
<br/>1. 打开Web Station如图所示新建虚拟主机
<br><img src="https://raw.githubusercontent.com/nikleechan/eb/master/webstation.png"><br>
<br/>2. 打开群辉控制面板-安全性-证书
<br/>点击新建-添加新证书-导入证书-选择下载的私钥跟证书
<br/>证书下载地址
```
https://raw.githubusercontent.com/nikleechan/eb/master/mb3admin.com.cert.pem
https://raw.githubusercontent.com/nikleechan/eb/master/mb3admin.com.key.pem
```
<br><img src="https://raw.githubusercontent.com/nikleechan/eb/master/cert0.png"><br>
<br/>3. 保存后在配置中将mb3admin.com的证书设置为刚导入的的证书
<br><img src="https://raw.githubusercontent.com/nikleechan/eb/master/cert1.png"><br>


#### 劫持mb3admin伪站

如搭建伪站的NAS地址为10.0.0.10 则如下填写,根据自己实际情况修改,目的就是劫持域名到搭建的伪站上

    10.0.0.10 mb3admin.com
	
如有使用ipv6,请将ipv6地址一起加入,可以避免白嫖时而有效时而无效
<br/>举例OP.根据网络-接口-全局网络选项中的IPv6 ULA 前缀来填写
<br/>![](https://raw.githubusercontent.com/nikleechan/eb/master/ULA.png)
<br/>如我的是fd59:5890:1be9::/48 搭建伪站的的IP是10.0.0.10,末尾是10,所以如下填写
	
    fd59:5890:1be9::10 mb3admin.com
	
<br/>如在主路由劫持,无需其他设置,直接修改hosts即可
<br/>如有旁路由,可能需要额外在旁路由上修改hosts(可能,未尝试)
<br/>如没有在路由劫持,需修改将每个客户端劫持到伪站

0. OP 梅林类路由可以直接在路由中直接修改hosts文件
<br/>登陆ssh输入以下命令
`vi /etc/hosts`
<br/>i 进入编辑状态
<br/>添加 `10.0.0.10 mb3admin.com`
`:wq` 保存退出
<br/>登陆OP-网络-DHCP/DNS-HOSTS 和解析文件 保存并应用
1. 群辉可以直接登录修改
<br/>登陆ssh输入以下命令
`vi /etc/hosts`
<br/>i 进入编辑状态
<br/>输入 `10.0.0.10 mb3admin.com`
`:wq` 保存退出
2. Windows修改只是路径不同
<br/>直接打开`C:\Windows\System32\drivers\etc\`目录
<br/>修改文件夹中的hosts文件
	
### 接下来运行这条脚本


以root用户执行命令：<br/>
</p><pre><code>wget -N --no-check-certificate "https://raw.githubusercontent.com/nikleechan/eb/master/embyonekey.sh" && chmod +x embyonekey.sh && ./embyonekey.sh</code></pre>

<br/>运行完毕
<br/>可以输入以下命令测试
```
nginx -t
```
查询是否报错

```
curl https://mb3admin.com/admin/service/registration/validateDevice
curl https://mb3admin.com/admin/service/registration/validateDevice/666
```
ssh中运行命令查看是否正确返回值

#### 祝大家玩得开心

<br/>如图,打开即可拥有会员黄标
<br/>
<br/>![](https://raw.githubusercontent.com/nikleechan/eb/master/ko.png)
<br/>
<br/>在Emby Premiere中输入任何秘钥都可以激活成功
<br/>
<br/>![](https://github.com/nikleechan/eb/blob/master/ko1.png)

#### 客户端证书安装
如服务器正常白嫖后,客户端还是无法正确显示,一般是证书不正确,请在客户端安装证书
```
https://raw.githubusercontent.com/nikleechan/eb/master/guomi.cer 
```
下载此链接文件名为guomi.cer的证书文件后安装相应设备上

Windows请安装此目录下
<br/>![](https://github.com/nikleechan/eb/blob/master/window.png)

<br/>IOS需要安装后在设置--通用--关于手机--证书信任设置中把证书信任


## 感谢 时光轴 星辰 不会魔法的思思 教程引路
https://imrbq.cn/exp/emby_hack.html

证书申请
国密网址：https://www.gmcert.org/subForm

<br/>![](https://github.com/nikleechan/eb/blob/master/shiguangzhou.png)

<br/>![](https://github.com/nikleechan/eb/blob/master/shiguangzhou1.png)

说明：
国密证书（guomi.crt）即文件mb3admin.com.cert.pem内容中的第二部分
 如：mb3admin.com.cert.pem内容为：
-----BEGIN CERTIFICATE-----
MIIEIjCCAwqgAwIBAgIJAL0OjFdDMG5hMA0GCSqGSIb3DQEBCwUAMGgxCzAJBgNV
BAYTAkNOMRAwDgYDVQQIDAdCZWlqaW5nMRAwDgYDVQQHDAdIYWlEaWFuMRMwEQYD
VQQKDApHTUNlcnQub3JnMSAwHgYDVQQDDBdHTUNlcnQgUlNBIFJvb3QgQ0EgLSAw
MTAeFw0yMDA0MjQwNTI5NDRaFw0yMjA3MjcwNTI5NDRaMGIxCzAJBgNVBAYTAkpQ
MQ4wDAYDVQQIDAVKYXBhbjEOMAwGA1UEBwwFSmFwYW4xDTALBgNVBAoMBEVtYnkx
DTALBgNVBAsMBEVtYnkxFTATBgNVBAMMDG1iM2FkbWluLmNvbTCCASIwDQYJKoZI
hvcNAQEBBQADggEPADCCAQoCggEBAL9FmcD4mDR1wnCHOZilVRaCLg64NomIXEiN
fwNqOPW2U/DnboR2fa622LWcH1iQf+obFQK0VmLXuUe3NVpn9+Vpbk9cZRReVabt
aKl5w1KmvNwm1BFJDbJPGa4+/VOq8oFDDjo7wYwrF1zftJSnF6xb6bTqXonX4mDN
bWxSa3dGIZvr6pQj3r76aUE7f02aTRAtviQwYubb2GFhH7LAO1sXmNqwgRwOc6bK
mOni2A5UqEfCXYXKreCV8SMsCnKwnouuiHKtqfcahxwP3sIEdZgZfmu8vJsp3UpW
oQyG/mzaGAyHnOYgNKEBUy99yY+s4MKdyvNwgt8gabiD2UhX/AkCAwEAAaOB1DCB
0TAMBgNVHRMBAf8EAjAAMAsGA1UdDwQEAwIEsDAdBgNVHSUEFjAUBggrBgEFBQcD
AQYIKwYBBQUHAwIwLAYJYIZIAYb4QgENBB8WHUdNQ2VydC5vcmcgU2lnbmVkIENl
cnRpZmljYXRlMB0GA1UdDgQWBBQ+f1MSSccxoTzcd9QhhajKjGcsOjAfBgNVHSME
GDAWgBSaJ+ucgJPLDenDPdFqehzisZ846TAnBgNVHREEIDAeggxtYjNhZG1pbi5j
b22CDioubWIzYWRtaW4uY29tMA0GCSqGSIb3DQEBCwUAA4IBAQBD+DfR63WB9tPx
AGjlB0oF+5Xp39w4msnE/rp0dcxhY0Sz77yzJPcA2Uo47aVN/OZluyXG31ZaCV9X
z+tiwjytLGXtFLpKEeiFOEI9YNw1JnnlzGg41FNWJmDN5I28k2dWK228ibjuCUrN
IY3gnlGX8hfeOcZWJjbPWnbQHquu3EL4DtDYZt8JbFyhhJhYJp2RodLImIOX2n0I
dxish1OyjyRK55CdH76C5K3zRhx9bZyrvXivo1t3FPxV+p/LyboVPC5jT7qRhYKZ
4AiUEml4lPibuaQsqDUCcvK/JcH1jXsei7Q6TxQQW4RJXd9kZOvL8Lc2smC34lxv
0bD5Ua5a
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIDsDCCApigAwIBAgIJAMjrH5w5KmnFMA0GCSqGSIb3DQEBCwUAMGgxCzAJBgNV
BAYTAkNOMRAwDgYDVQQIDAdCZWlqaW5nMRAwDgYDVQQHDAdIYWlEaWFuMRMwEQYD
VQQKDApHTUNlcnQub3JnMSAwHgYDVQQDDBdHTUNlcnQgUlNBIFJvb3QgQ0EgLSAw
MTAeFw0xOTEwMjQxMjM3NDRaFw0zOTA3MTExMjM3NDRaMGgxCzAJBgNVBAYTAkNO
MRAwDgYDVQQIDAdCZWlqaW5nMRAwDgYDVQQHDAdIYWlEaWFuMRMwEQYDVQQKDApH
TUNlcnQub3JnMSAwHgYDVQQDDBdHTUNlcnQgUlNBIFJvb3QgQ0EgLSAwMTCCASIw
DQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBANCpZk/j4CIM2o2IiZHTsQA10LTN
fD/dV//kyn9QXQwpRpcgTLuYassucaDSvkS56+p7jRKMgD9ZnE4QNf3Ay/UEACYG
UH7OubZtigxJpLjS69dHfy3yqt8GSOKsfFu6VZ//QphFGw4NkkCYngOuxhmV7WU0
xNasollGGuzjBmp46/bev8aomkI33OxSXWna3oCn3BSScgkoyWJTNN1+EwCZANO3
FeKUyPMGOhi49QlV4OyUgCfGlFqhAGZAT/PMo8oPwwmyHrlyn+jqin7+qKVF9loc
Nle9YyBi7eZkDbSoAUOg2WFaDDRrPhUnNU+l2TqCP+uCgyxU74Lphj00v00CAwEA
AaNdMFswHQYDVR0OBBYEFJon65yAk8sN6cM90Wp6HOKxnzjpMB8GA1UdIwQYMBaA
FJon65yAk8sN6cM90Wp6HOKxnzjpMAwGA1UdEwQFMAMBAf8wCwYDVR0PBAQDAgEG
MA0GCSqGSIb3DQEBCwUAA4IBAQBcoJlabv5wgUj6tgbb3gUVYHKlQWr2aaPWg1Vs
ru5ExyPcEhyQ2XM5AdnOMjKiTikyPYwk1/K1tJSNN5AmCfdofWr4m074s+Rf/i+h
dBuh2vjZee9L/NV2ZRcxpwp9e561+JBXoHvZ0JHDBGQ0WYsJ+m9fRxCR12oIVWWv
SAjbyetRRO+oTvi3dX2OQUgJhflS4/cxQblYxgL5nMIa+MVamXUNNfwEk3TZh4K/
NgtQY5KraEUU7bCkbbKdX2r+njobTQpbBV8uZ/JwsNghx4gfB+3QrteVfceQ+ip+
CpEU9X3JD9WkxEVFKBa0Q+TllSny07of0cWmRuwZlLUruBJD
-----END CERTIFICATE-----


则根证书(guomi.crt)内容为
-----BEGIN CERTIFICATE-----
MIIDsDCCApigAwIBAgIJAMjrH5w5KmnFMA0GCSqGSIb3DQEBCwUAMGgxCzAJBgNV
BAYTAkNOMRAwDgYDVQQIDAdCZWlqaW5nMRAwDgYDVQQHDAdIYWlEaWFuMRMwEQYD
VQQKDApHTUNlcnQub3JnMSAwHgYDVQQDDBdHTUNlcnQgUlNBIFJvb3QgQ0EgLSAw
MTAeFw0xOTEwMjQxMjM3NDRaFw0zOTA3MTExMjM3NDRaMGgxCzAJBgNVBAYTAkNO
MRAwDgYDVQQIDAdCZWlqaW5nMRAwDgYDVQQHDAdIYWlEaWFuMRMwEQYDVQQKDApH
TUNlcnQub3JnMSAwHgYDVQQDDBdHTUNlcnQgUlNBIFJvb3QgQ0EgLSAwMTCCASIw
DQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBANCpZk/j4CIM2o2IiZHTsQA10LTN
fD/dV//kyn9QXQwpRpcgTLuYassucaDSvkS56+p7jRKMgD9ZnE4QNf3Ay/UEACYG
UH7OubZtigxJpLjS69dHfy3yqt8GSOKsfFu6VZ//QphFGw4NkkCYngOuxhmV7WU0
xNasollGGuzjBmp46/bev8aomkI33OxSXWna3oCn3BSScgkoyWJTNN1+EwCZANO3
FeKUyPMGOhi49QlV4OyUgCfGlFqhAGZAT/PMo8oPwwmyHrlyn+jqin7+qKVF9loc
Nle9YyBi7eZkDbSoAUOg2WFaDDRrPhUnNU+l2TqCP+uCgyxU74Lphj00v00CAwEA
AaNdMFswHQYDVR0OBBYEFJon65yAk8sN6cM90Wp6HOKxnzjpMB8GA1UdIwQYMBaA
FJon65yAk8sN6cM90Wp6HOKxnzjpMAwGA1UdEwQFMAMBAf8wCwYDVR0PBAQDAgEG
MA0GCSqGSIb3DQEBCwUAA4IBAQBcoJlabv5wgUj6tgbb3gUVYHKlQWr2aaPWg1Vs
ru5ExyPcEhyQ2XM5AdnOMjKiTikyPYwk1/K1tJSNN5AmCfdofWr4m074s+Rf/i+h
dBuh2vjZee9L/NV2ZRcxpwp9e561+JBXoHvZ0JHDBGQ0WYsJ+m9fRxCR12oIVWWv
SAjbyetRRO+oTvi3dX2OQUgJhflS4/cxQblYxgL5nMIa+MVamXUNNfwEk3TZh4K/
NgtQY5KraEUU7bCkbbKdX2r+njobTQpbBV8uZ/JwsNghx4gfB+3QrteVfceQ+ip+
CpEU9X3JD9WkxEVFKBa0Q+TllSny07of0cWmRuwZlLUruBJD
-----END CERTIFICATE-----


