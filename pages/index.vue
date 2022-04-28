<template>
  <div class="page">
    <div class="image">
      <img src="~/assets/images/bg-page.jpg" />
      <div v-if="!checkForm" @click="signForm">
        <img class="box-sign" src="~/assets/images/sign.jpg"/>
      </div>
    </div>
    <v-form v-if="checkForm" class="sign-form" v-model="valid">
      <v-text-field
        v-model="firstname"
        :rules="nameRules"
        :counter="10"
        label="ชื่อ"
        required
      ></v-text-field>
      <v-text-field
        v-model="lastname"
        :rules="nameRules"
        :counter="10"
        label="นามสกุล"
        required
      ></v-text-field>
        <v-btn
        class="mr-4"
        @click="submit"
      >
        ลงนามถวายพระพร
      </v-btn>
      <v-btn @click="clear">
        clear
      </v-btn>
    </v-form>
  </div> 
</template>

<script>
// import SignImage from '~/components/SignImage.vue'
export default {
  // components: { SignImage},
  name: 'IndexPage',
   data: () => ({
      valid: false,
      checkForm: false,
      firstname: '',
      lastname: '',
      nameRules: [
        v => !!v || '*Name is required',
        v => v.length <= 10 || 'Name must be less than 10 characters',
      ],
    }),
    methods: {
      // submit () {
      //   console.log(this.valid);
      //   if(this.valid == true){
      //     console.log(this.firstname);
      //     console.log(this.lastname);
      //      this.$router.push('/confirm');
      //   }else{
      //     this.nameRules
      //   }
      // },
      submit () {
        try{
           if(this.valid == true){
              let fd = new FormData();
              fd.append('firstname',this.firstname);
              fd.append('lastname',this.lastname);
            
            // const response = await this.$axios.post('/api/save', fd) 
            // this.$swal.fire({
            //     icon: 'success',
            //     title: 'บันทึกสำเร็จ',
            //     text: 'ระบบได้ทำการบันทึกข้อมูลของคุณแล้ว'
            // }).then( function(){
            //     window.location.href = '/employee';
            // });
            console.log(fd);
           this.$router.push('/confirm');
          }else{
            this.nameRules
          }
        }catch(err){
            this.$swal.fire({
                icon: 'error',
                title: 'บันทึกไม่สำเร็จ',
                text: 'มีข้อผิดพลาดที่ไม่คาดคิดเกิดขึ้น โปรดลองใหม่อีกครั้ง'
            })
            console.log(err);
        };
      },
      clear () {
        this.firstname = ''
        this.lastname = ''
      },
      signForm(v){
         this.checkForm = !this.checkForm;
      },
    },

 
}
</script>
<style scoped>
  .page{
    text-align: center;
  }
  .box-sign{
    position: absolute;
    bottom: 5px;
    left: 42%;
    cursor: pointer;
  }
  .image{
    position: relative;
  }
  .sign-form{
    /* border: 1px solid; */
    width: 700px;
    display: inline-block;
    padding: 1rem;
  }
</style>
