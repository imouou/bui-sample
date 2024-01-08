# BUI-Sample

> BUI 干净的单页工程模板示例，可以直接在Github开发，Fork当前项目即可

[进入官网预览模板](http://www.easybui.com/).

## 工程需要安装 Node 12+ 以上版本，建议在 node 16.x

```bash

# 安装依赖
npm install

# 运行调试，LINK扫码直接在手机操作预览
npm run dev

# 打包上架的 dist.zip
npm run build

```


## 接口跨域问题

跨域有2种处理方式；

1. 根据你的chrome版本，有不同的跨域方式，这个可以百度“打开跨域的chrome”，这种方式比较简单，不用起服务都能正常预览，缺点是不能手机调试；
2. 配置代理app.json 的方式，PC手机都能调试；

例如 接口地址为： http://www.easybui.com/demo/json/shop.json

```js
   bui.ajax({
      url:"http://www.easybui.com/demo/json/shop.json",
      data: {}
   }).then((result)=>{
      console.log(result)
   })
```

这种写法会出现跨域问题，可以通过配置 `app.json` 的 proxy 代理转发。

```js
{
   proxy: {
      "/demo": {
         "target": "http://www.easybui.com",
         "changeOrigin": true,
         "ssl": false
      }
   }
}
```

接口请求地址要变更为相对路径，所有以 demo开头的接口，都会触发代理。注意：demo/ 是关键字，且前面不能加 ”/“ <del>/demo/</del>

```js
   bui.ajax({
      url:"demo/json/shop.json",
      data: {}
   }).then((result)=>{
      console.log(result)
   })
```

为了后续上架变更为正式环境，一般会在接口前加上一个变量；

```js
   // 正式环境
   // var urlpath = "http://www.easybui.com/";
   // 跨域调试环境
   var urlpath = "";

   bui.ajax({
      url: `${urlpath}demo/json/shop.json`,
      data: {}
   }).then((result)=>{
      console.log(result)
   })
```