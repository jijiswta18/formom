<template>
    <div class="image">
          <img src="~/assets/images/bg-page.jpg" />
          <!-- <div class="box-sign"> -->
            <NuxtLink to="/"><img class="box-sign" src="~/assets/images/sign.jpg" /></NuxtLink> 
          <!-- </div> -->
         
          <!-- <v-btn elevation="2"></v-btn> -->
    </div>
</template>
<style scoped>
    .box-sign{
        position: absolute;
        bottom: 0;
    }
    .image{
        position: relative;
    }
</style>