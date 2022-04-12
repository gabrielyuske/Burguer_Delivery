<template>
  <div id="main-banner">
    <h1>Make your burger</h1>
  </div>
</template>

<script>
export default {
  name: "Banner"
}
</script>

<style scoped>
  #main-banner{
    background-image: url("food_copy.jpg");
    background-position: right;
    background-repeat:  no-repeat;  
    width: auto; 
    /* border: 10px; */
    background-color: black;                      
    background-size: 50% ;                              
    height: 600px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }
  #main-banner h1 {
    margin-left: 20px;
    color:#FFF;
    text-align: center;
    font-size: 60px;
    background-color: #222;
    padding: 20px 40px;
    border-color: white;
    border-style: solid;
     border-color: white;
  }

</style>