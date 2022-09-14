<template>
  <div class="home" >
   
   <div style="background-color: black">
    <p class="p"> News</p>
   </div>
   <Cards />
  </div>
</template>

<script>
import Cards from '@/components/Cards.vue'

export default {
  name: 'HomeView',
  components: {
    Cards
}
}
</script>
<style>
 
  .p{
    font-size: 100px;
    color:white;
    animation: slidein 7s infinite ;
  }
  @keyframes slidein {
  from {
    margin-right:10px;
  }

  to {
   margin-left: 100%;
  }
}
  
</style>
