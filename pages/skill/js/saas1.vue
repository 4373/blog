<style scoped>
  .view {
    color: white;
    font-weight: bold
  }

  .view p {
    margin: 0px 0;
    border-bottom: 1px solid #eee;
    border-radius: 8px
  }
  .box{
    width: 200px;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.2);
    padding: 8px;
    border-radius: 8px;
  }
  .parent{
    color: #999;
    font-size: 12px;
    cursor: pointer;
  }
  .icon{
    margin-right: 4px;
  }
  .children{
    /* padding-left: 10px; */
    color: #666;
  }
  .child{
    padding: 6px 16px;
    cursor: pointer;
  }
  .child:hover{
    background: #f8f8f8;
  }
</style>
<template>
  <div>
    <!-- <h2 class="title">SaaS项目 结后总结1</h2> -->
    <p class="text-center">2018-08-13 by me</p>

    <h4>概况</h4>
    <p>从去年九月开始到今年7月，做了个SaaS项目。这个项目基本是独立完成，包括环境的搭建，权限的设计，单据的打印等。总之写完之后还是收获了很多，如今赶上开始写博客，正好记录下来。</p>
    <p>这个项目是用vue-cli脚手架搭建的单页面应用。 其中包括一些vue的周边vue-router， vuex。ui使用的是element-ui，而数据请求使用的是axios， 还有一些特定功能使用到了e-charts，xlsx，wangEditor，cropperjs等。</p>

    <h4>目录结构</h4>
    <p>此项目的目录结构如下:</p>
    <img src="~assets/saas/folder.jpg" alt="">
    <p>相比与vue-cli默认生成的， 这里多了api、common、directive、less、mixins文件夹，对于文件来说添加了一个echart-theme.js和iview-theme.js， 分别是e-charts.js和iview
      的主题配置文件。对于iview-theme.js，是由于历史原因，之前选择ui的是iview，后面由于总总原因换成了element，但现在有几个复杂的页面依然使用着iview的组件，要抽离出来成本太高，遂放弃。
    </p>
    <ul>
      <li>api目录，顾名思义，放的是后端提供的全部api。</li>
      <li>common目录，一些通用的js。</li>
      <li>directive目录，vue指令。</li>
      <li>less目录，样式文件。</li>
      <li>mixins目录，一些相似页面的混入。</li>
    </ul>
    <h4>页面结构</h4>
    <p>页面结构主要是router.js文件了，该文件导出了两个对象一个router， 一个routes。</p>
    <div>
      <pre>
        <code class="language-javascript">
          // router.js

          // routes
          export const routes = [
            { 
              path: '/role', 
              name: '角色管理', 
              component: { render(h) {return h('router-view')}}, 
              icon: 'life',
              children: [
                {path: '/role/list', component: RoleList, name: '角色列表', hidden: true},
                {path: '/role/deal', component: RoleDeal, name: '角色处理'},
                {path: '/role/detail', component: RoleDetail, name: '角色详情'},
              ]
            },
            { 
              path: '/account', 
              name: '帐号管理', 
              component: { render(h) {return h('router-view')}}, 
              icon: 'user',
              children: [
                {path: '/account/list', component: AccountList, name: '账号列表'},
                {path: '/account/deal', component: AccountDeal, name: '账号处理'},
                {path: '/account/detail', component: AccountDetail, name: '账号详情'},
              ]
            },
            ...otherMenu
          ]

          // router
          export const router = new Router({
            routes: [
              { path: '/', component: Home, children: route },
              { path: '/login', component: Login },
              ...others,
              { path: '/404', component: Page404 },
            ]
          })
          
        </code>
      </pre>
    </div>
    <p>导出的router不用多说， 是vue实例化所需要的路由对象，而routes的话， 在本项目中主要用来遍历菜单的侧边栏，对于每一个item，你可以加一些你需要的字段，比如该菜单栏的字体图标，亦比如你目前在开发一个新的模块，但你现在这个入口不想对外公布，你所需要做的就是加一个hidden字段就可以了，一切需求就由你自由发挥了。</p>
    <p>如果菜单template是这样子的：</p>
    <pre class="language-markup">
      <code class="language-markup" v-text='html'>

      </code>
    </pre>
    <p>那么最终渲染出来就是这个样子了：</p>
    <div class="box">
      <div class="parent" v-for = '(item, key) in routes' :key='key'>
        <div class="parent-name">
          <Icon :type='item.icon'></Icon>
          <span>{{item.name}}</span>
          <div class="children">
            <p class="child" v-for = '(i, k) in item.children' :key='k' v-if='!i.hidden' :title='i.path'>{{i.name}}</p>
          </div>
        </div>
      </div>
    </div>
    <p>可以看到字体图标渲染出来，并且角色列表隐藏了。</p>
    <p>导出的routes结合后端传过来的权限列表，可以过滤出该用户的权限菜单，这个会在权限篇具体讨论。</p>
    <p>根据router.js内容生成的页面结构如下：</p>
    <div class="view ">
      <p class="bg-primary pa-1">主页</p>
      <p class="bg-danger pa-1 ml-3">角色管理</p>
      <p class="bg-info pa-1 ml-5">角色列表</p>
      <p class="bg-info pa-1 ml-5">角色新增或编辑</p>
      <p class="bg-info pa-1 ml-5">角色详情</p>
      <p class="bg-danger pa-1 ml-3">帐号管理</p>
      <p class="bg-info pa-1 ml-5">列表</p>
      <p class="bg-info pa-1 ml-5">新增或编辑</p>
      <p class="bg-info pa-1 ml-5">详情</p>
      <p class="bg-primary pa-1">登录页</p>
      <p class="bg-primary pa-1">活动页或html5页面</p>
      <p class="bg-primary pa-1">404</p>
      <p class="bg-primary pa-1">500</p>
    </div>
    <p>蓝色是顶层页面， 主要包括登陆页，404，500 等不需要登陆的页面，也可以做一些活动页面，移动web页面。以及项目的主页home，项目的主要功能都写在这里面。红色就是菜单项，里面会包含该菜单项的功能页面，也就是灰色部分。灰色部分不会出现在菜单栏，同通过点击红色项redirect到该项下面的列表页，该菜单项的其他部分的入口全在列表页里面。</p>
    <p>如此一来页面就显得非常可控了</p>
    <h4>组件处理</h4>
    <p>本项目大部分组件都可以在element-ui里面找到，而有一些特定的功能需要自己写一些组件，对此。我们在components 文件夹中创建一个index.js，用来引入需要自己写的组件和element的组件。具体如下：</p>
    <pre>
      <code class="language-javascript">
          // /components/index.js
          import Vue from 'vue'
          import './element'
          import '../less/element-variables.scss'
          
          import ikv from './kv.vue'
          Vue.component('ikv', ikv)

          import backtop from './backtop.vue'
          Vue.component('ibacktop', backtop)

          import loading from './loading.vue'
          Vue.component('iloading', loading)

          import table from './fixtable.vue'
          Vue.component('itable',  table)
          ....
          // main.js
          import '/components/index.js'
      </code>
    </pre>
    <p>对于element，有很多组件在本项目中是用不到的，于是采用按需加载。同时，我们可能有一种需求，就是对组件的默认行为或样式有适应本项目的需求。而element提供的全局配置比较少，但我们可以手动的为需要的组件改动一些配置，创建一个elemengt.js：</p>
    <pre>
      <code class="language-javascript">
          import Vue from 'vue'
          import {
            Button,
            InputNumber,
            Message,
            // Notification
            ...
          } from 'element-ui'


          // 修改默认的设置
          Button.props.plain.default = true
          Button.props.type.default = 'primary' // 偷个懒， 因为每次写 &lt;el-button type='primary'&gt;&lt;/el-button&gt; 加一个type很麻烦
          InputNumber.props.controlsPosition.default = 'right'
          // 改写方法，谨慎尝试，建议看着源码来
          InputNumber.methods = Object.assign({},InputNumber.methods, {
            handleInputChange(value) {
              const newVal = value === '' ? 0 : Number(value);
              if (!isNaN(newVal) || value === 0) {
                this.setCurrentValue(newVal);
              }
            }
          })
          Vue.use(Button)
          Vue.use(InputNumber)
          Vue.use(Message)
          // Vue.use(Notification)
          ...

          //  this.$message({type: 'info', message: '提示'}) 的调用方式改为 this.$mes.info('提示')
          const mes = ['info', 'success', 'error', 'warning']
          Vue.prototype.$mes = {}
          mes.forEach(item => {
            Vue.prototype.$mes[item] = (mes) => {
              Message({
                type: item,
                message: mes
              })
            }
          })
      </code>
    </pre>
    <p>考虑到在每个页面都要引入常用的组件，所以把组件注册在全局。</p>
    <h4>接口配置</h4>
    <p>接口配置主要是对接口进行统一的管理和全局的拦截。由于后端是属于重构项目，接口的变动非常频繁，如果将每个接口的请求地址写在各自的页面的话，后续修改接口将会是一场灾难。于是统一的接口管理就应运而生。接口的写法大体是这样：</p>
    <pre>
      <code class="language-javascript">
        export const login = [
          { name: 'getToken', url: '/api/auth/weblogintoken', method: 'POST' },
          { name: 'login', url: '/api/auth/in', method: 'POST' },
          { name: 'logout', url: '/api/auth/out', method: 'GET' }
        ]
      </code>
    </pre>
    <p></p>
  </div>
</template>
<script>
  export default {
    layout: 'home',
    data() {
      return {
        routes: [
            { 
              path: '/role', 
              name: '角色管理', 
              component: { render(h) {return h('router-view')}}, 
              icon: 'life',
              children: [
                {path: '/role/list', component: 'RoleList', name: '角色列表', hidden: true},
                {path: '/role/deal', component: 'RoleDeal', name: '角色处理'},
                {path: '/role/detail', component: 'RoleDetail', name: '角色详情'},
              ]
            },
            { 
              path: '/account', 
              name: '帐号管理', 
              component: { render(h) {return h('router-view')}}, 
              icon: 'user',
              children: [
                {path: '/account/list', component: 'AccountList', name: '账号列表'},
                {path: '/account/deal', component: 'AccountDeal', name: '账号处理'},
                {path: '/account/detail', component: 'AccountDetail', name: '账号详情'},
              ]
            }
          ],
          html: `
          <div class="parent" v-for = '(item, key) in routes' :key='key'>
            <div class="parent-name">
              <svg class="icon" aria-hidden="true">
                  <use :xlink:href="'#' + item.icon"></use>
              </svg>
              <span>{{item.name}}</span>
              <div class="children">
                <p class="child" v-for = '(i, k) in item.children' :key='k' v-if='!i.hidden' :title='i.path'>{{i.name}}</p>
              </div>
            </div>
          </div>
          `
      }
    },
    mounted() {

    }
  }
</script>
