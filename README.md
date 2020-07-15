# taval

## 首页

- 引入一些基本的 css 文件（一般基本的(reset.css)，处理移动端的(border.css)，iconfont）
- 引入 iconfont 并使用:(https://www.iconfont.cn)
- 使用 stylus，并设置全局变量（例如颜色，高度等）安装`stylus`和`stylus-loader`
- 定义css中的全局变量在`src\assets\styles\varibles.styl`
- 修改路径引入，以@代表 src 目录为例，修改 style 路径

`webpack.base.conf.js`

```javascript
 resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      'styles':resolve('src/assets/styles')
    }
  },
```

- 引入 fastclick 处理移动端点击事件，安装`fastclick`
- 先把 header 做出来
- 轮播图 `vue-awesome-swiper@2.6.7` （https://github.com/surmon-china/vue-awesome-swiper）
- 图标展示，图标滑动展示，使用 `vue-awesome-swiper`,计算图标页数并展示特定的图标，使用计算属性
- 推荐部分，写 css 代码，嘤嘤嘤，看来 css 还得再搞搞，不然布局不好看,定义全局处理文字过长显示省略号在`src\assets\styles\mixins.styl`
- 周末去哪部分通过修改推荐部分来完成
- 数据通过 ajax 获取，数据放在`/static/mock`目录下
- 修改`config\index.js`目录下 inde.js 来使`axios.get("/api/index.json").then(this.getHomeInfoSucc);`,/api 可以访问到本地静态资源目录

```javascript
     proxyTable: {
      '/api': {
        target: 'http://localhost:8080',
        pathRewrite: {
          '^/api': '/static/mock'
        }
      }
    },
```

- 在 Home.vue 文件里同意获取所有数据，通过父子组件传值传到各个其他组件里，头部的城市暂时传入一个固定值，也通过父子组件传值传过去
- 页面挂在就发出请求

> A Vue.js project

## Build Setup

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
