<template>
  <Navbar :logo="logo_src" :alt="app_name"/>
  <router-view/>
  <Footer />
</template>

<script>
import Navbar from "./components/Navbar.vue"
import Footer from "./components/Footer.vue"
export default {
  components:{
    Navbar,
    Footer
  },
  data(){
    return{
      logo_src: "img/burger.png",
      app_name: "Your only Burger"
    }
  }
}
</script>
<style>
*{
  font-family: Helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.main_container{
  margin: 50px;
  min-height: 345px;
}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>
