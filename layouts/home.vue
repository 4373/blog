<style>
  body,
  html {
    background: #eee;
    margin: 0;
    padding: 0;
    font-size: 14px;
    color: #665577
  }

  * {
    box-sizing: border-box;
  }

  .index-layout {
    display: flex;
    margin: 1vh;
    padding: 16px;
    border-radius: 10px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    min-height: 98vh;
    background: white;
  }

  .layout-left {
    padding: 8px;
    flex: 0 0 180px;
    border-right: 1px solid #eee;
  }

  .layout-right {
    padding: 8px;
    flex: 1 1 auto;
    overflow: auto
  }
  .head{
    margin-bottom: 16px
  }
  .position{
    vertical-align: middle
  }
  .position-item{
    padding: 0 16px;
    border-left: 1px solid #ddd;
    color: #888;
  }
  .position-item:first-of-type{
    border-left: none;
    padding-left:0;
  }
  .home-box{
    padding: 0 48px
  }
  @media screen and (max-width: 414px) {
    .layout-left {
      flex: 0 0 0px!important;
      border-right: 0px solid #eee;
      overflow: hidden;
    }
    .home-box{
      padding: 0px
    }
  }
</style>
<template>
  <div class="index-layout">
    <div class="layout-left">
      <img src="~static/logo.png" alt="" height=80>
    </div>
    <div class="layout-right">
      <div class="head clearfix">
          <div class="left">
              <span class="position-item">
                  <Icon type='home'></Icon>
                <span class='ml-1'>首页</span>
              </span>
              <span class="position-item">
                  <Icon type='js'></Icon>
                <span class='ml-1'>JS</span>
              </span>
              <span class="position-item">
                  <Icon type='article'></Icon>
                <span class='ml-1'>this 的一切</span>
              </span>
          </div>
          <div class="right">
              <svg class="icon" aria-hidden="true">
                  <use xlink:href="#icon-user"></use>
              </svg>
          </div>
      </div>
      <div class="home-box">
          <nuxt></nuxt>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    head: {
      link: [
        { rel: 'stylesheet', href: '//at.alicdn.com/t/font_789693_qhjr2o02p8.css' },
        { rel: 'stylesheet', href: '/prismjs/prism.css' },
      ],
      script: [
        { src: '//at.alicdn.com/t/font_789693_m7bduh5vm.js' },
        // { src: '/prismjs/prism.js'}
      ]
    },
    data() {
      return {}
    },
    mounted() {
      setTimeout(() => {
        const script = document.createElement('script')
        script.src = '/prismjs/prism.js'

        document.body.appendChild(script)
      }, 0)
    }
  }
</script>
