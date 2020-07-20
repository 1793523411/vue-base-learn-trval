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

## 城市选择页

+ 完成头部，点击城市跳转到城市页，点击返回箭头返回首页
+ 完成搜索框，主要是一个布局
+ 完成搜索框的布局
+ 完成城市，热门城市，城市列表的布局，以及右侧字母表的显示
+ 引入`better-scroll`，实现上下滑动的流畅动画
+ 通过ajax动态获取数据并传递给子组件
+ 右侧字母实现触摸滑动到对应的字母，使用一个属性记录是否处于触摸状态，使用clientY，动态计算所触摸的字母的下标（（触摸处距离顶部距离-A距离顶部距离）/ ，每个字母的高度），这里使用letters替换了原来的cities，优化点：1.使用update钩子获取satrtY，因为StartY是固定不变的，不需要每次都获取，只需在ajax取回数据后更新时获取一次startY即可2.加一个定时器timer实现函数节流，控制touchmove函数执行频率
+ 实现搜索框搜索功能，用watch观察keyword的变化，并使用timer进行函数节流，父子组件传值获取城市数据，动态讲符合的数据传入要渲染的数组，v-show控制搜索结果的显示，使用better-scroll是显示的搜索结果偶可以滑动显示，具有滑动动画

## 使用Vuex

+ 使用vuex管理城市，初步联调两个页面，city和首页，读取，修改store的公共数据实现联调，初步使用了Vuex
+ 利用本地存储解决刷新数据改变为原始的数据(同步数据和异步数据，这里都是同步数据，没有action的必要)，在store中使用localStorage来存储数据，同时为了避免用户禁止本地存储的功能，从而导致异常从而整个代码不能运行，要对本地存储的操作进行异常的捕获
+ store目录下的index一般很复杂，所以需要讲state和mutations分开写入到不同的文件
+ vuex提供了`import {mapState, mapMutations} from 'vuex'`这种方法，可以更方便的进行数据获取，和修改数据

```javascript
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  methods: {
    handleCityClick(city){
      // this.$store.dispatch('changeCity',city)
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
```
+ vuex还提供了getter方法，这有点类似于计算属性,书写在代码里（学习使用，对项目代码无用），使用如下(与state使用类似)

```javascript
import {mapGetters} from 'vuex'

computed: {
  ...mapGetters(['doubleCity])
}

```
## 优化

+ 每次路由切换都会重新发生请求，这样会导致效率很低，每次页面切换都会因加载资源而闪烁，所以可以使用vue自带的keep-alive包裹住router-view，来进行优化，该操作会进行缓存，并增加一个actived的钩子函数，每回页面跳转，actived都会执行，但mounted不会执行
+ 切换城市后要进行发送请求，在actived中进行判断，对比上一次获取的城市和从vuex中新获取，若不同则进行再次发送请求，带上新的参数，否则什么也不做

## 详情页

+ 制作顶部的banner，一张图片+一些文字，首先实现路由跳转，然后进行布局
+ 制作画廊组件，利用better-scroll，实现点击开启画廊，点击关闭画廊，进行css布局
+ 坑：子组件向父组件传递事件，会冒泡，导致只能打开，不能关闭，解决：在子组件点击处加.stop来阻止时间继续传递

```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```
+ 详情页顶部banner渐隐渐现效果，和返回按钮返回首页，通过监听scroll计算opacity属性
+ 全局事件绑定会出现许多bug,应该进行解绑（多出来的active会在进入页面执行，也会增加一个deactivated离开页面执行，如果不解绑，任何页面都会触发该事件）
```javascript
  activated(){
   window.addEventListener('scroll',this.handleScroll)
  },
  deactivated(){
    window.removeEventListener('scroll',this.handleScroll)
  }
```
+ 然而代码中原来只这样写的，并不会达到正确的效果，因为离开页面后事件并没有解绑，bug依然存在

```javascript
  mounted() {
    window.addEventListener('scroll',this.handleScroll)
    // console.log('+++++')
  },
  unmounted(){
    window.addEventListener('scroll',this.handleScroll)
    // console.log('--------')
  }
```
+ 递归组件实现层级菜单（组件的名字可以递归时用），数据要有父组件传过来，直接在子组件里写数据递归时会报错
+ 使用ajax获取数据，动态传递路由参数，发出请求
+ 由于vue-router使用keep-alive进行了缓存，所以动态路由不起作用，可以使用activated进行解决，也可以在在keep-alive标签上加： `<keep-alive exclude="Detail">`,name为组件中定义的name
+ 解决页面跳转视图停留位置的bug，页面跳转后总是没有回到顶部，所以在router中加入

```javascript
  scrollBehavior (to, from, savedPosition) {
    return { x: 0, y: 0 }
  }
```


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
