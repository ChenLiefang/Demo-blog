请求相关的头：
User-Agent 用户代理字符串，可以读到浏览器的内核，版本，所在操作系统的版本等信息
Host 浏览器是用什么域名进行的该次http请求
  因为一个服务器上可以有多个网站，不同的网站域名不同，但此种情况下ip是相同的
  对于客户端来说，连接的ip就是相同的，而ip是在连接之前就解析的，在tcp/ip层服务器是不知道对方用什么域名连接的自己
  GET /index.html HTTP/1.1
  Host: lily.github.io
Referer 当前请求的资源取回来后被哪个页面使用
  当前资源的引用者是哪个页面。
  可以实现   防 盗链
    即如果服务器通过此头发现资源返回后是被别家网站使用，则可以：
      返回空内容；或者返回一个版权声明的图片（仅对图片请求适用）
  由于会把当前用户地址栏里的完全地址发给资源所在服务器，
  有一定的隐私风险，现在可以通过一些手段禁止浏览器发Referer头
Accept 可以接受的资源的媒体类型，其中q的值代表期望值的大小
Accept-Encoding 可以接受的资源的响应体的压缩算法
Accept-Language 期望接收的页面的自然语言的语种。q同上
Content-Type 请求体/响应体的媒体类型及编码方式
  text/html; charset=UTF-8
  application/javascript; charset=UTF-8
  application/json; charset=UTF-8
  image/jpeg
  image/webp
If-Modified-Since/Last-Modified 协商缓存 协商成功的话返回304状态码
If-None-Match/ETag 协商缓存              协商成功的话返回304状态码
Content-Length 请求体的长度
Connection: keep-alive 协商承载该http请求的tcp连接的状态,以在同一个tcp上执行多个http请求/响应
  需要配合Content-Length使用.
  Pipeline 管线化请求/响应
    即无需等待响应收到后再在同一个连接上发下一个请求
    而是可以一次性把所有请求都发过去
    等待所有响应按序收到

响应相关的头：
Date 日期
Content-Encoding 响应体的压缩算法
Content-Length 响应体的长度（如果压缩则是压缩之后的长度）
Content-Type 响应体的媒体类型及编码方式
ETag 响应体的哈希值
Last-Modified 本资源的最后修改时间
Server 服务器所使用的软件，一般服务器是不会响应这个头的
  因为如果某个服务器软件有漏洞，这么做相当于告诉别人服务器有漏洞
Expires 本资源的过期时间，在这个过期时间之前，浏览器重新使用这个资源时可以不发请求
Accept-Range：bytes
Referrer-Policy: origin-when-cross-origin, strict-origin-when-cross-origin
  设置浏览器发送Referer策略
  只需要在html（即页面）的响应头里设置
Transfer-Encoding: chunked 响应数据的传输方式，一段一段的发。
  当服务器无法预测响应体长度时使用。
  当使用这个功能时，一个tcp上就只能走这一个http请求了。tcp连接断开时响应结束。
  有这个头时就没有Content-Length了
content-disposition: attachment; filename="index.html"
  该响应头触发浏览器弹出下载对话框，并在对话框里填写默认文件名为filename
X-Frame-Options  设置本页面能否被放入其它页面的iframe
  deny 完全不允许被放入任何iframe
  same-origin 可以被放入同源页面的iframe里
Content-Security-Policy 内容安全策略，只对html页面响应，设置本页面的各项安全相关的配置
    default-src 'none';

    base-uri 'self';

    block-all-mixed-content;
    禁用所有混合内容（即https页面里的http内容）

    connect-src 'self' uploads.github.com www.githubstatus.com collector.githubapp.com api.github.com www.google-analytics.com github-cloud.s3.amazonaws.com github-production-repository-file-5c1aeb.s3.amazonaws.com github-production-upload-manifest-file-7fdce7.s3.amazonaws.com github-production-user-asset-6210df.s3.amazonaws.com cdn.optimizely.com logx.optimizely.com/v1/events wss://alive.github.com;
    页面里的js能够连接的目标服务器（ajax，其它方式的连接如websocket）

    font-src github.githubassets.com;
    页面能够加载的字体来源

    form-action 'self' github.com gist.github.com;
    表单能够提交到的目标服务器

    frame-ancestors 'none';
    谁能做为本页面的frame祖先

    frame-src render.githubusercontent.com;
    本页面的iframe可以加载来自哪里的页面

    img-src 'self' data: github.githubassets.com identicons.github.com collector.githubapp.com github-cloud.s3.amazonaws.com *.githubusercontent.com customer-stories-feed.github.com spotlights-feed.github.com;
    图片能够加载来自哪里的

    manifest-src 'self';
    manifest能够加载来自哪里的

    media-src 'none';
    media能够加载来自哪里的

    script-src github.githubassets.com;
    脚本能够加载来自哪里的 <div onclick="alert(2)"></div>

    style-src  github.githubassets.com;
    样式能够加载来自哪里的 <div style="color:red";

    worker-src github.com/socket-worker.js gist.github.com/socket-worker.js
    worker的代码能够加载来自哪里的
Cache-Control 缓存控制。可以做为请求头，也可以做为响应头
  提供对缓存策略的精细控制，
  内容可以是给浏览器看的，也可以是给服务器看的，还可以是给中间服务器看的。

断点续传
Accept-Range：bytes
Range: 10000-99999


