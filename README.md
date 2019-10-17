# 多页面项目快速搭建

## 项目设置

```
# 安装依赖
npm install
```

### Compiles and hot-reloads for development

```
# 运行开发服务
npm run serve
```

### Compiles and minifies for production

```
# 打包编译项目
npm run build
```

### Run your tests

```
npm run test
```

### Lints and fixes files

```
npm run lint
```

### Run your unit tests

```
npm run test:unit
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

---

## 项目说明

### 环境变量配置

&emsp;&emsp;根目录下环境变量配置文件`.env.dev`,在`npm run serve`启动开发环境服务的时候加载.在项目中可以通过`process.env.VUE_APP_TEST_URL`获取到测试环境的地址.此变量的作用:1. 接口代理,请求测试环境接口. 2. 访问测试服务器中的静态资源.如果只是在个人的开发环境下需要改变这个地址,可以创建一个`.env.dev.local`文件来覆盖

- 环境变量配置文件 (_\.local 的文件会被 git 忽略_):

  - `.env` 全局环境变量配置
  - `.env.local` 全局环境个人的变量配置
  - `.env.dev` 开发环境变量配置
  - `.env.dev.local` 开发环境个人的变量配置

- 可配置的环境变量:

  - `NODE_ENV` 判断生产环境或开发环境
  - `VUE_APP_TEST_URL` 开发环境请求的资源地址
  - `OUTPUT_DIR` 项目编译输出的静态资源目录
  - `VIEWS_PATH` 项目编译输出的 html 模板文件目录

### 服务器地址及文件目录

服务器 IP: 120.27.130.7
服务器域名:
服务器静态文件目录: `/data/www/lighttpd/geelyjkd/public/jkd`
服务器 php 模板文件目录: `/data/www/lighttpd/geelyjkd/resources/views`

### 服务端 git 地址

```bash
> git@192.168.11.206:xiangmu/geelyjkd.git
```

### 框架、工具库文档链接

框架
[vue](https://cn.vuejs.org)

vue 插件
[vuex](https://vuex.vuejs.org/zh/guide/)
[vue-router](https://router.vuejs.org/zh/)
[vue-echarts](https://github.com/ecomfe/vue-echarts)
[vue-cookies](https://github.com/cmp-cc/vue-cookies)

UI 库
[element-ui](http://element-ui.cn/#/zh-CN/)

工具库
[axios](https://www.kancloud.cn/yunye/axios/234845)
[echarts](https://www.echartsjs.com/zh/)
[dayjs](https://github.com/iamkun/dayjs)

### 目录结构

```
│ .env                        // 全局环境变量配置
│ .env.dev                    // 开发环境变量配置
│ package.json
│ vue.config.js               // vue项目配置
│
├─ public
│
├─ src
│   ├─ theme-variables.scss     // element-ui主题变量配置文件
│   ├─ app
│   │   └─ jkd                     // 健康度前台页面
│   │       │ App.vue
│   │       │ main.js
│   │       │ router.js
│   │       ├─ store               // vuex配置
│   │       ├─routes                  // 路由模块
│   │       └─views
│   │
│   ├─assets
│   │   ├─images                // 公共图片资源
│   │
│   ├─components                // 公共组件
│   │
│   ├─lib
│   │ ├─element-variables.scss  // element-ui基础主题变量文件
│   │ └─axios.js                // axios配置文件
│   │
│   ├─styles                     // 公共样式文件
│   │   │  variable.scss         // 公共样式变量配置文件
│   │   │  mixins.scss           // 公共mixin配置文件
│   │   └─ font                 // 公共字体图标
│   └─theme                     // element-ui主题文件
│
└─tests
└─unit
```

### element-ui 自定义主题构建

1. 初始化基础主题变量文件

```
  # 默认生成的文件在`src/lib/element-variables.scss`.可在package.json中配置
  npm run theme-init
```

2. 修改 src 目录下的 theme-variables.scss 文件

3. 编译主题文件

```
  # 默认生成的主题文件在`src/theme`目录下.可在package.json中配置
  npm run theme-build
```

### 多页面配置说明

如需配置多页面.需要在``vue.config.js 中配置 pages 字段.开发环境访问多页面路由时,需要在`devServer`中修改配置:

```javascript
module.exports = {
  //...
  devServer: {
    open: false,
    disableHostCheck: true,
    proxy,
    historyApiFallback: {
      // 在此处添加要访问的页面路由.如不添加这项.那么访问admin页面时,需要写完整的admin.html
      rewrites: [{ from: /^\/admin/, to: '/admin.html' }]
    }
  }
  //...
}
```
