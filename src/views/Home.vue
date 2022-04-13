<template>
<div>
  <Banner />   
    <div class="main_container">
      <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
      <h1>Monte o seu BURGER</h1>
      <BurgerForm />
    </div>
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
