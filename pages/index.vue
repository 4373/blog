<style>
  body {
    background: #22cdd6
  }
  a {
    text-decoration: none;
    cursor: pointer;
    color: #f5f5f5
  }
  *::selection{
    background: rgba(0, 0, 0, 0.3);
    color: #22cdd6
  }
  a:hover {
    text-decoration: underline
  }

  .tekst {
    color: #32413d;
    font-family: 'Lato', arial, sans-serif;
    text-transform: uppercase;
    font-size: 14px;
    line-height: 28px;
    font-weight: bold;
    display: block;
    letter-spacing: 2px;
    max-width: 100%;
    position: absolute;
    bottom: 20px;
    left: 30px;
    z-index: 1
  }
  .head{
    height: 300px;
    /* background: orangered */
    text-align: center;
    margin-top: 20vh;
  }
  .title{
    font-size: 32px;
    padding: 16px;
    margin-bottom: 32px;
    color: white;
    font-family: sans-serif;
    text-shadow: 3px 3px 0 rgba(104, 105, 100, 0.6);
    /* text-transform: uppercase; */
  }
  .input{
    height: 60px;
    width: 80%;
    background: #707473;
    color: white;
    outline: none;
    font-size: 24px;
    font-weight: bold;
    padding: 0 16px;
    border:none;
    text-align: center;
  }
</style>
<template>
  <div class="home">
    <div class="head">
      <div class="title">
          Sloth, like rust, consumes faster than labor wears.
      </div>
      <input type="text" class="input bs3" v-model='search'>
    </div>
    <!-- <p class="tekst">Design by
      <a href="https://dribbble.com/shots/2485177-Dancing" target="_blank">Eran Mendel</a>
    </p> -->
  </div>
</template>

<script>
  export default {
    layout: 'default',
    data() {
      return {
        search: `It's me , ${new Date().toLocaleDateString()}`
      }
    }
  }
</script>
