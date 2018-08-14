<style scoped>
  .view {
    color: white;
    font-weight: bold
  }

  .view p {
    margin: 2px 0;
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
              children: [
                {path: '/role/list', component: RoleList},
                {path: '/role/deal', component: RoleDeal},
                {path: '/role/detail', component: RoleDetail},
              ]
            },
            { 
              path: '/account', 
              name: '帐号管理', 
              component: { render(h) {return h('router-view')}}, 
              children: [
                {path: '/account/list', component: AccountList},
                {path: '/account/deal', component: AccountDeal},
                {path: '/account/detail', component: AccountDetail},
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
    <p>导出的router不用多说， 是vue实例化所需要的路由对象，而routes的话， 在本项目中主要用来遍历菜单的侧边栏，结合后端传过来的权限列表，可以过滤出该用户的权限菜单，这个会在权限篇具体讨论。</p>
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
      <p class="bg-primary pa-1">404</p>
      <p class="bg-primary pa-1">500</p>
    </div>
    <p>蓝色是顶层页面， 主要包括登陆页， 404， 500 等不需要登陆的页面，以及项目的主页home，项目的主要功能都写在这里面。红色就是菜单项，里面会包含该菜单项的功能页面，也就是灰色部分。灰色部分不会出现在菜单栏，同通过点击红色项redirect到该项下面的列表页，该菜单项的其他部分的入口全在列表页。</p>
  </div>
</template>
<script>
  export default {
    layout: 'home',
    mounted() {

    }
  }
</script>
