在这里创建一个workers脚本，内容如下

```shell
addEventListener("fetch", event => {
  let url = new URL(event.request.url);
  if (url.pathname == "/test" && url.search == "") {
    url.href="https://cachefly.cachefly.net/200mb.test"
    let request = new Request(url, event.request);
    event.respondWith(fetch(request));
  }
})
```

之后点击保存并部署，看到200的[http](https://so.csdn.net/so/search?q=http&spm=1001.2101.3001.7020)相应即可

接下来添加自定义域（custom domain）

不需要创建任何类型的实例，直接写出，例如0823.ppp.com，你只需要保证 ppp.com在你的CF上托管即可，证书会[自动配置](https://so.csdn.net/so/search?q=自动配置&spm=1001.2101.3001.7020)

保存之后就可以通过https://0823.ppp.com/test下载文件，其中/test你可以在脚本中自定义，这只是一个[重定向](https://so.csdn.net/so/search?q=重定向&spm=1001.2101.3001.7020)到https://cachefly.cachefly.net/200mb.test的监听脚本，你也可以用50mb
