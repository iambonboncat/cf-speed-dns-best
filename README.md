## 不懂写代码，也就是用返回的ip，直接在Cloudflare的workers上部署了下面的转接代码，然后绑二级域名，实现自动更新最快IP
```javascript
addEventListener("fetch", event => {
  // 获取请求的URL
  let url = new URL(event.request.url);

  // 设置新的目标域名
  url.hostname = "curl 'https://ip.164746.xyz/ipTop.html'"; // 替换为你要转接的目标域名
  url.protocol = 'https'; // 如果新域名使用HTTP协议，请改为'http'

  // 构建301重定向响应
  let response = Response.redirect(url.toString(), 301);

  // 返回重定向响应
  event.respondWith(response);
});
```
## cf-speed-dns是什么?
CloudflareSpeedTest 推送「每5分钟自选优选 IP」获取Cloudflare CDN 延迟和速度最快 IP ！

## cf-speed-dns有哪些功能？
* CloudflareSpeedTest优选IP，实时更新列表页面。[https://ip.164746.xyz](https://ip.164746.xyz)
* CloudflareSpeedTest优选IP，Top接口(默认)[https://ip.164746.xyz/ipTop.html](https://ip.164746.xyz/ipTop.html)；Top10接口[https://ip.164746.xyz/ipTop10.html](https://ip.164746.xyz/ipTop10.html)。
* DNSPOD实时域名解析推送，fork 本项目。
  * Action配置，Actions secrets and variables 添加 DOMAIN(例如：164746.xyz)，SUB_DOMAIN（例如：dns），SECRETID（xxxxx），SECRETKEY（xxxxx），PUSHPLUS_TOKEN（xxxxx）。
* DNSCF实时域名解析推送，fork 本项目。
  * Action配置，Actions secrets and variables 添加 CF_API_TOKEN(例如：xxxxx)，CF_ZONE_ID（例如：xxxxx），CF_DNS_NAME（dns.164746.xyz），PUSHPLUS_TOKEN（xxxxx）。
* 接入PUSHPLUS消息通知。[https://www.pushplus.plus/push1.html](https://www.pushplus.plus/push1.html)

## 接口请求
```javascript
curl 'https://ip.164746.xyz/ipTop.html'
```
## 接口返回
```javascript
104.16.204.6,104.18.103.125
```

## 感谢
[XIU2](https://github.com/XIU2/CloudflareSpeedTest)、[ddgth](https://github.com/ddgth/cf2dns)
