<script>
   export default {
    name: 'Loader',

     
  }
</script>
    
<template>


  <div>

    <span class="loader"></span>

  </div>


</template>

<style lang="scss" scoped>
@import '../../assets/scss/partials/variables';

div{
  min-height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.loader {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  display: block;
  margin:15px auto;
  position: relative;
  color: #FFF;
  left: -100px;
  box-sizing: border-box;
  animation: shadowRolling 2s linear infinite;
}

@keyframes shadowRolling {
  0% {
    box-shadow: 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0);
  }
  12% {
    box-shadow: 100px 0 $dark-color, 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0);
  }
  25% {
    box-shadow: 110px 0 $dark-color, 100px 0 $dark-color, 0px 0 rgba(255, 255, 255, 0), 0px 0 rgba(255, 255, 255, 0);
  }
  36% {
    box-shadow: 120px 0 $dark-color, 110px 0 $dark-color, 100px 0 $dark-color, 0px 0 rgba(255, 255, 255, 0);
  }
  50% {
    box-shadow: 130px 0 $dark-color, 120px 0 $dark-color, 110px 0 $dark-color, 100px 0 $dark-color;
  }
  62% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 130px 0 $dark-color, 120px 0 $dark-color, 110px 0 $dark-color;
  }
  75% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 130px 0 $dark-color, 120px 0 $dark-color;
  }
  87% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 130px 0 $dark-color;
  }
  100% {
    box-shadow: 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0), 200px 0 rgba(255, 255, 255, 0);
  }
}
   
</style>