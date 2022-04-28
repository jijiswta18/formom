<template>
  <div class="confirm-page">
     <div class="image">
       <!-- <SignImage/> -->
        <img src="~/assets/images/bg-page.jpg" />
        <!-- <NuxtLink to="/"><img class="box-sign" src="~/assets/images/sign.jpg" /></NuxtLink>  -->
    </div>
    <h2 class="mg-one">ด้วยเกล้าด้วยกระหม่อมขอเดชะ ข้าพระพุทธเจ้า</h2> 
    <h3 class="mg-two">นางสาวสวิตตา ศรีจันทร์</h3> 
    <p>ผู้ร่วมลงนามลำดับที่ : </p>
    <div class="box-footer">
         <v-btn
              color="warning"
              dark
              class="btn-home"
             @click="backHome"
            >
              กลับหน้าหลัก
            </v-btn>
             <v-btn
              color="warning"
              dark
              class="btn-print"
              @click="printDivContent"
            >
             พิมพ์คำถวายพระพร
            </v-btn>
           
    </div>
   

  </div>
  
</template>

<script>
import SignImage from '~/components/SignImage.vue'
export default {
  components: { SignImage},
  name: 'IndexPage',
   data: () => ({
      valid: false,
      firstname: '',
      lastname: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
    }),
    methods: {
      backHome () {
          this.$router.push('/');
      },
      printDivContent () {
        window.print()
        // this.$refs.observer.reset()
      },
    },

 
}
</script>
<style scoped>
 
  .image{
    position: relative;
  }
  .btn-home{
      background-color: #0170c2!important;
      color: white;
  }
   .btn-print{
     background-color: white!important;
      color: #0170c2!important;
      border: 1px solid#0170c2!important;
  }
  .mg-one{
      margin-top: 2rem;
      margin-bottom: 1rem;
  }
  .mg-two{
      margin-top: 2rem;
      margin-bottom: 1rem;
  }
  .box-footer{
    margin: 2rem 0;
  }
  @media print {
  .box-footer{
    display: none;
  }
}

</style>
