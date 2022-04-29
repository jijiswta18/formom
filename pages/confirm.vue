<template>
  <div class="confirm-page">
     <div class="image">
        <img src="~/assets/images/bg-page.jpg" />
    </div>
    <h2 class="style-title">ด้วยเกล้าด้วยกระหม่อมขอเดชะ ข้าพระพุทธเจ้า</h2> 
    <h3 class="style-name">{{item.p_name}} {{item.p_lastname}}</h3> 
    <p class="style-number">ผู้ร่วมลงนามลำดับที่ : {{item.p_id}}</p>
    <div class="box-footer">
         <v-btn
            rounded
            class="btn btn-home"
            @click="backHome"
            >
              กลับหน้าหลัก
            </v-btn>
             <v-btn
              rounded
              class="btn btn-print"
              @click="printDivContent"
            >
             พิมพ์คำถวายพระพร
            </v-btn>
           
    </div>
   

  </div>
  
</template>

<script>
export default {
  name: 'IndexPage',
   data: () => ({
      item:{
        p_name: 'สวิตตา',
        p_lastname: 'ศรีจันทร์',
        p_id: '100',
      }
    }),
  created(){
    this.getDetail()
  },
  methods: {
    backHome () {
        this.$router.push('/');
    },
    printDivContent () {
      window.print()
    },
    getDetail: async function(){
        // const response = await this.$axios.post('/api/company/get') 
        // this.item = response
    }
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
    margin-right: 0.5rem;
    font-weight: 300;
  }
   .btn-print{
    background-color: white!important;
    border: 1px solid #0170c2!important;
    color: #0170c2;
    font-weight: 400;
   
  }
  .style-title{
    font-weight: 400;
    margin: 2rem 0 1rem 0;
  }
  .style-name{
   margin: 2rem 0 1rem 0;
   font-weight: 400;
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
