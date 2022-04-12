<template>
  <Banner />   
  <div class="main_container">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <h1>HOME</h1>
    <BurgerForm />
  </div>
</template>

<script>
// @ is an alias to /src
import Banner from "../components/Banner.vue"
import BurgerForm from "../components/Burgerform.vue"
export default {
  name: 'Home',
  components: {
    Banner,
    BurgerForm
  }
}
</script>
