<template>
  <div class="page">
    <div class="image">
      <img src="~/assets/images/bg-page.jpg" />
      <div v-if="!checkForm" @click="signForm">
        <img class="box-sign" src="~/assets/images/banner01.gif"/>
      </div>
    </div>
    <v-form v-if="checkForm && !checkSubmit" class="sign-form" v-model="valid">
      <v-text-field
        v-model="p_name"
        :error-messages="nameErrors"
        :counter="10"
        label="Name"
        required
        @input="$v.p_name.$touch()"
        @blur="$v.p_name.$touch()"
      ></v-text-field>
      <v-text-field
        v-model="p_lastname"
        :error-messages="lastnameErrors"
        :counter="10"
        label="Name"
        required
        @input="$v.p_lastname.$touch()"
        @blur="$v.p_lastname.$touch()"
      ></v-text-field>
      <div class="btn-submit" @click="submit">
        <img src="~/assets/images/banner01.gif" />
      </div>
    </v-form>
    <div v-if="checkSubmit"  class="box-detail">
      <h2 class="style-title">ด้วยเกล้าด้วยกระหม่อมขอเดชะ ข้าพระพุทธเจ้า</h2> 
      <h3 class="style-name"></h3> 
      <p class="style-number">ผู้ร่วมลงนามลำดับที่ : </p>
      <div class="box-footer">
          <a href="https://www.cgd.go.th/">
            <v-btn
              rounded
              class="btn btn-home"
              >
              กลับหน้าหลัก
            </v-btn>
          </a>
          <v-btn
            rounded
            class="btn btn-print"
            @click="printDivContent"
          >
          พิมพ์คำถวายพระพร
        </v-btn>    
      </div>
    </div>
  </div> 
</template>

<script>
import moment from 'moment'
import { validationMixin } from 'vuelidate'
import { required, maxLength} from 'vuelidate/lib/validators'
export default {
  mixins: [validationMixin],
  name: 'IndexPage',
  validations: {
    p_name: { required, maxLength: maxLength(10) },
    p_lastname: { required, maxLength: maxLength(10) },
  },
  data: () => ({
    valid: false,
    checkForm: false,
    checkSubmit: false,
    name: '',
    p_name: '',
    p_lastname: '',
    p_festival: 'forking',
    regis_date: moment().format('YYYY-MM-DD HH:mm:ss'),
    browser: '',
    device: '',
  }),
    computed:{
      nameErrors () {
        const errors = []
        if (!this.$v.p_name.$dirty) return errors
        !this.$v.p_name.maxLength && errors.push('Name must be at most 10 characters long')
        !this.$v.p_name.required && errors.push('Name is required.')
        return errors
      },
      lastnameErrors () {
        const errors = []
        if (!this.$v.p_lastname.$dirty) return errors
        !this.$v.p_lastname.maxLength && errors.push('Name must be at most 10 characters long')
        !this.$v.p_lastname.required && errors.push('Name is required.')
        return errors
      },
    },
    created(){
      this.getDeviceType();
      this.getBrowserDetect();
      this.$axios.setHeader('Content-Type', 'application/json', [
        'post'
      ])
    },
    methods: {
      submit: async function(){
        if(this.p_name && this.p_lastname){
          this.checkSubmit = true
          let fd = {
            "name" : this.p_name,
            "lastname" : this.p_lastname,
            "p_festival" : this.p_festival,
            "regis_date" : this.regis_date,
            "browser" : this.browser,
            "device" : this.device,
          }
          const response = await this.$axios.$post('/api/for-king', fd) 
          console.log(response);
        }else{
          this.$v.$touch()
        }
      },
    
      signForm(v){
         this.checkForm = !this.checkForm;
      },
   
      getBrowserDetect(){        
        let userAgent = navigator.userAgent;
        let browserName;   
        if(userAgent.match(/chrome|chromium|crios/i)){
          browserName = "chrome";
        }else if(userAgent.match(/firefox|fxios/i)){
          browserName = "firefox";
        } else if(userAgent.match(/safari/i)){
          browserName = "safari";
        }else if(userAgent.match(/opr\//i)){
          browserName = "opera";
        } else if(userAgent.match(/edg/i)){
          browserName = "edge";
        }else{
          browserName="No browser detection";
        }
        this.browser = browserName
      },
      
      getDeviceType(){
          let ua = navigator.userAgent;
          let deviceName;
          if (/(tablet|ipad|playbook|silk)|(android(?!.*mobi))/i.test(ua)) {
            deviceName = "tablet";
          }else if( /Mobile|iP(hone|od)|Android|BlackBerry|IEMobile|Kindle|Silk-Accelerated|(hpw|web)OS|Opera M(obi|ini)/.test(ua)){
            deviceName = "mobile";
          }else{
            deviceName = "desktop";
          }
          this.device = deviceName  
      },
      printDivContent () {
        window.print()
      },
    }
}
</script>
<style scoped>
  .page{
    text-align: center;
  }
  .box-sign{
    position: absolute;
    bottom: 10px;
    cursor: pointer;
    margin-left: auto;
    margin-right: auto;
    left: 0;
    right: 0;
    text-align: center;
  }
  .image{
    position: relative;
  }
  .sign-form{
    max-width: 700px;
    display: inline-block;
    padding: 1rem;
    width: 100%;
  }
  .btn-submit{
    cursor: pointer;
    display: inline-block;
  }
  ::v-deep .v-messages__message{
    color: red!important;
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
  a{
   text-decoration: none;
  }
  @media only screen and (max-width: 600px) {
    .image img{
      width: 100%;
    }
}
</style>
