> 寄语：在强者的眼里没有弱者的席位
>
> 摘自《超兽武装》



> 本文已收录至[https://github.com/likekk/-Blog](https://github.com/likekk/-Blog)欢迎大家star :smile::smile: :smile: ，共同学习，共同进步。如果文章有错误的地方，欢迎大家指出。后期将在将GitHub上规划前端学习的路线和资源分享。



### 写在前面

每一篇文章都希望您有所收获，每一篇文章都希望您能静下心来浏览、阅读。每一篇文章都是作者精心打磨的作品。

【**原创不易、请勿白嫖**】。如果您觉得二郎神杨戬有点东西的话，作者希望你可以帮我点亮那个点赞的按钮，对于二郎神杨戬这个暖男来说，**真的真的非常重要**，这将是我持续写作的动力。您只需要小手轻轻一点，带来的却是温暖了这个作者，给予他前进的动力。



### 前言

通过上一篇博客的学习，我相信读者们也简单了解Vue的生命周期和它主要的8个钩子函数，对于里面的一些概念，大叫可以多读几遍，细细揣摩一下。那么本文主要是搭建vue-cli项目。这也将是后期我们需要学习的重点，一般做项目的时候都是以vue-cli项目为前提的。搭建项目的过程可能有许多插图。



### 环境搭建

单页Web应用（single page web application，SPA），就是只有一张Web页面的应用，是加载单个HTML 页面并在用户与应用程序交互时动态更新该页面的Web应用程序。

提供一个官方命令行工具，可用于快速搭建大型单页应用（SPA）。该工具为现代化的前端开发工作流提供了开箱即用的构建配置。只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目：

```javascript
# 全局安装 vue-cli
＄ npm install --global vue-cli
# 创建一个基于 webpack 模板的新项目
＄ vue init webpack my-project
# 安装依赖
＄ cd my-project
＄ npm install
＄ npm run dev
```



1、安装node.js

从[Node.js官网](https://nodejs.org/)下载并安装Node，安装过程很简单，一路“下一步”就可以了。安装完成之后，打开命令行工具(win+r，然后输入cmd)，输入 node -v，如下图，如果出现相应的版本号，则说明安装成功。

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227090911526-34144813.png)

如果安装不成功，可以直接把安装包修改成压缩包，解压后配置环境变量也可以，就成了绿色版。

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227090709541-1804525284.png)

2、修改npm为淘宝镜像

因为npm的仓库有许多在国外，访问的速度较慢，建议修改成cnpm，换成taobao的镜像

```javascript
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

安装这里是因为我们用的npm的服务器是外国，有的时候我们安装“依赖”的时候会很慢很慢，所以就用这个cnpm来安装我们说需要的“依赖”。安装完成之后输入 cnpm -v，如下图，如果出现相应的版本号，则说明安装成功。

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227091708635-2018470631.png)



3、安装webpack

安装webpack，打开命令行工具输入：

```javascript
npm install webpack -g
```

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227092111557-2133066784.png)



安装完成之后输入

```javascript
webpack -v
```

如下图，如果出现相应的版本号，则说明安装成功。

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227092155854-468013152.png)



4、安装vue-cli脚手架构建工具

打开命令行工具输入：

```
cnpm install vue-cli -g
```

安装完成之后输入 vue -V（注意这里是大写的“V”），如下图，如果出现相应的版本号，则说明安装成功。

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227093502729-1372950933.png)



### 构建项目

1、在硬盘上找一个文件夹放工程用的。这里有两种方式指定到相关目录：

- cd 目录路径

- 如果以安装git的，在相关目录右键选择Git Bash Here

2、安装vue脚手架输入：vue init webpack projectName，注意这里的“projectName” 是项目的名称可以说是随便的起名，但是“不能用中文”。

提示选择项：

```javascript
$ vue init webpack exprice --------------------- 这个是那个安装vue脚手架的命令
This will install Vue 2.x version of the template. ---------------------这里说明将要创建一个vue 2.x版本的项目
For Vue 1.x use: vue init webpack#1.0 exprice
? Project name (exprice) ---------------------项目名称
? Project name exprice
? Project description (A Vue.js project) ---------------------项目描述
? Project description A Vue.js project
? Author Datura --------------------- 项目创建者
? Author Datura
? Vue build (Use arrow keys)
? Vue build standalone
? Install vue-router? (Y/n) --------------------- 是否安装Vue路由，也就是以后是spa（但页面应用需要的模块）
? Install vue-router? Yes
? Use ESLint to lint your code? (Y/n) n ---------------------是否启用eslint检测规则，这里个人建议选no
? Use ESLint to lint your code? No
? Setup unit tests with Karma + Mocha? (Y/n)
? Setup unit tests with Karma + Mocha? Yes
? Setup e2e tests with Nightwatch? (Y/n)
? Setup e2e tests with Nightwatch? Yes
vue-cli · Generated "exprice".
To get started: --------------------- 这里说明如何启动这个服务
cd exprice
npm install
npm run dev
```

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227094909057-1168210976.png)



3、cd 命令进入创建的工程目录，首先cd projectName

4、安装项目依赖：npm install，因为自动构建过程中已存在package.json文件，所以这里直接安装依赖就行。不要从国内镜像cnpm安装(会导致后面缺了很多依赖库)，但是如果安装时间过长，那么就使用：cnpm install 吧

5、安装 vue 路由模块 vue-router 和网络请求模块 vue-resource，输入：

>  cnpm install vue-router vue-resource --save

![](https://images2018.cnblogs.com/blog/63651/201712/63651-20171225202633697-49547651.png)

文件目录说明

```xml
|-- build                            // 项目构建(webpack)相关代码
|   |-- build.js                     // 生产环境构建代码
|   |-- check-version.js             // 检查node、npm等版本
|   |-- dev-client.js                // 热重载相关
|   |-- dev-server.js                // 构建本地服务器
|   |-- utils.js                     // 构建工具相关
|   |-- webpack.base.conf.js         // webpack基础配置
|   |-- webpack.dev.conf.js          // webpack开发环境配置
|   |-- webpack.prod.conf.js         // webpack生产环境配置
|-- config                           // 项目开发环境配置
|   |-- dev.env.js                   // 开发环境变量
|   |-- index.js                     // 项目一些配置变量
|   |-- prod.env.js                  // 生产环境变量
|   |-- test.env.js                  // 测试环境变量
|-- src                              // 源码目录
|   |-- components                     // vue公共组件
|   |-- store                          // vuex的状态管理
|   |-- App.vue                        // 页面入口文件
|   |-- main.js                        // 程序入口文件，加载各种公共组件
|-- static                           // 静态文件，比如一些图片，json数据等
|   |-- data                           // 群聊分析得到的数据用于数据可视化
|-- .babelrc                         // ES6语法编译配置
|-- .editorconfig                    // 定义代码格式
|-- .gitignore                       // git上传需要忽略的文件格式
|-- README.md                        // 项目说明
|-- favicon.ico 
|-- index.html                       // 入口页面
|-- package.json                     // 项目基本信息
```



6、启动项目，输入：npm run dev。服务启动成功后浏览器会默认打开一个“欢迎页面”，如下图：

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227095057073-1165044851.png)



编译成功后可以直接在浏览器中查看项目：

![](https://images2017.cnblogs.com/blog/63651/201712/63651-20171227095249948-1785617410.png)



### WebStorm搭建Vue-cli项目

1、打开WebStrom，选择Create New Project这个选项

![](https://img2018.cnblogs.com/blog/1475945/201908/1475945-20190811000355931-2106402184.png)



2、选择搭建Vue.js项目，填写项目文件位置，Node.js版本，选择vue-cli，项目的模板，选好之后，点击Next

![](https://img2018.cnblogs.com/blog/1475945/201908/1475945-20190811000621927-763685541.png)



3、慢慢的的等待一段之间之后，就会出现如下界面。然后直接点击Next

![](https://s1.ax1x.com/2020/06/07/t2aQn1.png)



4、然后傻瓜式的安装，一直Next下去，直到到达这个界面。是否安装vue-router，这里我们选择Yes，点击Next

![](https://s1.ax1x.com/2020/06/07/t2aKXR.png)



5、是否安装ESLint，这里我们暂时不安装，你需要安装的话也可以。

![](https://s1.ax1x.com/2020/06/07/t2amp4.png)



6、后面询问是否安装啥东西的时候，我们一律不安装，傻瓜式点击Next，最后项目的目录结构如下。

![](https://s1.ax1x.com/2020/06/07/t2an1J.png)

对于每一个文件的目录说明，之前已经说过了，这里就不过多的重复了，右侧有个npm选项，

直接双击dev或者start。控制台可以输入



> npm run start 或者
>
> npm run dev

配置的脚本从package.json里面有



7、启动项目，如果出现如下界面，那么使用WebStorm搭建Vue-cli项目实现了。

![](https://s1.ax1x.com/2020/06/07/t2auc9.png)



### Vue-cli项目引入jQuery和Bootstrap

jQuery和BootStrap在Vue-cli项目中使用的并不多，但是有些公司可能会使用到，所以在这里还是需要介绍一下。



1、添加依赖

项目根目录下找到package.json 添加

- "bootstrap": "^3.3.6"
- "jquery": "^2.1.4"

对于版本，自己可以自行选择。



2、安装依赖

- cnpm install
- npm install

安装完成之后我们去node_modules查看是否安装成功，安装成功之后的结果

![](https://img2018.cnblogs.com/i-beta/1475945/201912/1475945-20191221143846301-616447359.png)

![](https://img2018.cnblogs.com/i-beta/1475945/201912/1475945-20191221143911863-1550936174.png)



3、导入jQuey和Bootstrap

在main.js 导入 （注意导入是node_modules下的路径可以点进去查看具体位置）min是压缩后文件建议导入这个

```javascript
import 'jquery/dist/jquery.min.js'
import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.min.js' 
```



main.js文件

```javascript
// The Vue build version to load with the `import` command
// (runtime-only or standalone) has been set in webpack.base.conf with an alias.
import Vue from 'vue'
import store from './store/index'
// import router from './router'
// import router from './router/hello'
// import  router from './router/test'
// import  router from './router/common'
// import router from './router/one'
import router from './router/two'
import 'jquery/dist/jquery.min'		//	引入jQuery
import 'bootstrap/dist/js/bootstrap.min'	//	引入bootstrap脚本
import 'bootstrap/dist/css/bootstrap.min.css'	//	引入bootstrap样式
Vue.config.productionTip = false
/* eslint-disable no-new */
new Vue({
  el: '#app',
  router,
  components: {},
  template: ''
})
```



4、使用内置插件ProvidePlugin自动加载模块

项目运行，浏览器控制台会输出如下信息，此时jQuery并未依赖成功，将提示错误:

![](https://img2018.cnblogs.com/i-beta/1475945/201912/1475945-20191221144113689-1550178027.png)

在build/webpack.base.conf.js中增加插件配置

```javascript
const webpack = require('webpack')
```

添加配置

```
plugins: [
  new webpack.ProvidePlugin({
    $: "jquery",
    jQuery: "jquery",
    "windows.jQuery": "jquery"
  })
],
```

build下webpack.base.conf.js的完整结果

```javascript
'use strict'
const path = require('path')
const utils = require('./utils')
const config = require('../config')
const vueLoaderConfig = require('./vue-loader.conf')
const webpack =require('webpack')	//	新增
function resolve (dir) {
  return path.join(__dirname, '..', dir)
}



module.exports = {
  context: path.resolve(__dirname, '../'),
  entry: {
    app: './src/main.js'
  },
  output: {
    path: config.build.assetsRoot,
    filename: '[name].js',
    publicPath: process.env.NODE_ENV === 'production'
      ? config.build.assetsPublicPath
      : config.dev.assetsPublicPath
  },
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
    }
  },
  module: {
    rules: [
      {
        test: /\.vue$/,
        loader: 'vue-loader',
        options: vueLoaderConfig
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        include: [resolve('src'), resolve('test'), resolve('node_modules/webpack-dev-server/client')]
      },
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('img/[name].[hash:7].[ext]')
        }
      },
      {
        test: /\.(mp4|webm|ogg|mp3|wav|flac|aac)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('media/[name].[hash:7].[ext]')
        }
      },
      {
        test: /\.(woff2?|eot|ttf|otf)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 10000,
          name: utils.assetsPath('fonts/[name].[hash:7].[ext]')
        }
      }
    ]
  },
  plugins: [	//	新增
    new webpack.ProvidePlugin({
      $: "jquery",
      jQuery: "jquery",
      "windows.jQuery": "jquery"
    })
  ],
  node: {
    // prevent webpack from injecting useless setImmediate polyfill because Vue
    // source contains it (although only uses it if it's native).
    setImmediate: false,
    // prevent webpack from injecting mocks to Node native modules
    // that does not make sense for the client
    dgram: 'empty',
    fs: 'empty',
    net: 'empty',
    tls: 'empty',
    child_process: 'empty'
  }
}
```

到这里WebStrorm引入jQuery和BootStrap的全部步骤就结束了，剩下就是在项目中如何使用了。



### Vue-cli项目引入Vant(移动端)

vant作为之前自己移动端商城项目的首选框架，可以是老伙计了，如果你想做一个webapp商城的话，那么这个vant是绝对不能错过的。

官网：[vant](https://youzan.github.io/vant/#/zh-CN/)

#### 安装

1、npm安装

在现有项目中使用 Vant 时，可以通过`npm`或`yarn`安装

```javascript
# 通过 npm 安装
npm i vant -S

# 通过 yarn 安装
yarn add vant
```



#### 引入Vant

1、引入方式一(自动按需引入组件)

babel-plugin-import是一款 babel 插件，它会在编译过程中将 import 的写法自动转换为按需引入的方式

```javascript
npm i babel-plugin-import -D
```

```javascript
// 在.babelrc 中添加配置
// 注意：webpack 1 无需设置 libraryDirectory
{
  "plugins": [
    ["import", {
      "libraryName": "vant",
      "libraryDirectory": "es",
      "style": true
    }]
  ]
}

// 对于使用 babel7 的用户，可以在 babel.config.js 中配置
module.exports = {
  plugins: [
    ['import', {
      libraryName: 'vant',
      libraryDirectory: 'es',
      style: true
    }, 'vant']
  ]
};
```

在src/component目录下新建一个IndexComponent.vue，然后使用Vant的一些组件

```javascript
<template>
    <div>
      <van-button type="default">默认按钮</van-button>
      <van-button type="primary">主要按钮</van-button>
      <van-button type="info">信息按钮</van-button>
      <van-button type="warning">警告按钮</van-button>
      <van-button type="danger">危险按钮</van-button>
    </div>
</template>

<script>
  import {Button} from 'vant' // 导入按钮组件
    export default {
        name: "IndexComponent",
      components:{
        [Button.name]: Button // 注册组件
      }
    }
</script>

<style scoped>

</style>

```



2、引入方式二(手动按需引入组件)

在不使用插件的情况下，可以手动引入需要的组件

```javascript
import Button from 'vant/lib/button';
import 'vant/lib/button/style';
```



3、引入方式三(导入所有组件)

Vant 支持一次性导入所有组件，引入所有组件会增加代码包体积，因此不推荐这种做法

```
import Vue from 'vue';
import Vant from 'vant';
import 'vant/lib/index.css';

Vue.use(Vant);
```



4、引入方式四(通过 CDN 引入)

使用 Vant 最简单的方法是直接在 html 文件中引入 CDN 链接，之后你可以通过全局变量`vant`访问到所有组件。

```javascript
<!-- 引入样式文件 -->
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/vant@2.8/lib/index.css"
/>

<!-- 引入 Vue 和 Vant 的 JS 文件 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vant@2.8/lib/vant.min.js"></script>

<script>
  // 在 #app 标签下渲染一个按钮组件
  new Vue({
    el: '#app',
    template: `<van-button>按钮</van-button>`,
  });

  // 调用函数组件，弹出一个 Toast
  vant.Toast('提示');

  // 通过 CDN 引入时不会自动注册 Lazyload 组件
  // 可以通过下面的方式手动注册
  Vue.use(vant.Lazyload);
</script>
```



### Vue-cli项目引入element ui（PC端）

element-ui是我在开发中会使用到的PC端框架，目前正在做的这个项目也在使用element-ui这个框架

官网：[element-ui](https://element.eleme.cn/#/)

#### 安装

npm安装

```javascript
npm i element-ui -S
```



CDN安装

```javascript
<!-- 引入样式 -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!-- 引入组件库 -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```

#### 引入Element-ui

引入的话这里有两种方法供你选择，这里推荐使用按需引入，打包项目的时候可以减少项目的体积，

1、全局引入

在 main.js 中写入以下内容：

```javascript
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

以上代码便完成了 Element 的引入。需要注意的是，样式文件需要单独引入。



2、按需引入

借助 babel-plugin-component，我们可以只引入需要的组件，以达到减小项目体积的目的

首先，安装 babel-plugin-component：

```javascript
npm install babel-plugin-component -D
```

然后，将 .babelrc 修改为：

```javascript
{
  "presets": [
    ["env", {
      "modules": false,
      "targets": {
        "browsers": ["> 1%", "last 2 versions", "not ie <= 8"]
      }
    }],
    "stage-2"
  ],
  "plugins": ["transform-vue-jsx", "transform-runtime",[
    "component",
    {
      "libraryName": "element-ui",
      "styleLibraryName": "theme-chalk"
    }
  ]]
}
```

接下来，如果你只希望引入部分组件，比如 Button 和 Select，那么需要在 main.js 中写入以下内容：

```javascript
import Vue from 'vue';
import { Button, Select } from 'element-ui';
import App from './App.vue';

Vue.component(Button.name, Button);
Vue.component(Select.name, Select);
/* 或写为
 * Vue.use(Button)
 * Vue.use(Select)
 */

new Vue({
  el: '#app',
  render: h => h(App)
});
```

接下来就可以使用这里面的任意组件了

参考链接：

https://www.cnblogs.com/best/p/8124786.html

https://element.eleme.cn/

https://youzan.github.io/vant/#/zh-CN/



### 结尾

如果觉得本篇文章对您有用的话，可以麻烦您给笔者点亮那个点赞按钮。
<img src="https://s1.ax1x.com/2020/03/23/8oGjfA.th.jpg">

对于杨戬这个暖男来说：**真的真的非常有用**，您的支持将是我继续写文章前进的动力，我们下篇文章见。

**【原创】|二郎神杨戬**

> 原创不易，莫要白嫖。
> 二郎神杨戬，一个在互联网前端苟且偷生的划水程序员，专注于前端开发，善于技术分享。
> 如需转载，请联系作者或者保留原文链接，微信公众号搜索二郎神杨戬或者扫描下方的二维码更加方便。
>
> 一起来见证二郎神杨戬的成长吧！更多好文、技术分享尽在下方这个公众号。欢迎关注。

<img src="https://s1.ax1x.com/2020/05/04/Y9LspR.png" />