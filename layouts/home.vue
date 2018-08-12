<style>
  body, html{
    background: #eee;
    margin: 0;
    padding: 0;
  }
  * {
    box-sizing: border-box
  }
.index-layout{
  display: flex;
  margin: 1vh;
  padding: 16px;
  border-radius: 10px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2); 
  min-height: 98vh;
  background: white;
}
.layout-left{
  padding: 8px;
  flex: 0 0 180px;
  border-right: 1px solid #eee;
}
.layout-right{
  padding: 8px
}
</style>
<template>
  <div class="index-layout">
    <div class="layout-left">
      <img src="~static/logo.png" alt="" height= 80>
      
    </div>
    <div class="layout-right">
      <nuxt></nuxt>
    </div>
  </div>
</template>