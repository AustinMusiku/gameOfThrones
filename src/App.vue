<template>
  <div class="hero">
  </div>
  <Characters/>
  <Footer/>
</template>

<script>
import Characters from './components/Characters'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    Characters,
    Footer
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html{
  scroll-behavior: smooth;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
}
.hero{
  display: grid;
  place-items: center;
  width: 100%;
  height: 80vh;
  background: url('https://4.bp.blogspot.com/-_AWOHYbG3ZQ/XOPN77M-JJI/AAAAAAAADCc/HOnXC92F1N4Hncd71pdDXj8K_m_eBvmQQCKgBGAs/w1920-h1080-c/game-of-thrones-iron-throne-uhdpaper.com-4K-75.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;

}
</style>
