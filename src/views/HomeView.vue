<template>
  <div class="home" >
    <p class="p"> News</p>
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
    
    animation: slidein 5s infinite ;
  }
  @keyframes slidein {
  from {
    margin-right:10px;
  }

  to {
   margin-left: 40%;
  }
}
  
</style>
