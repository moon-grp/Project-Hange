<template>
<div class="search-cnt">
    <div class="inner-cnt">
   <h1>Weather Forcast</h1>
   <h3>Enter the city name you want us to forecast</h3>
       <form :form="form" class="form-cnt"  @submit.prevent='onsubmit'>
             <a-form-item>
         <a-input
         v-decorator="[
         'text',
         {rules:[{required:true, message:'Please input a city!'}]}
         ]"
          size="large" v-model="text" 
           style="height: 50px"
            placeholder="Enter City..."/>
            </a-form-item>
          <a-button class="btn-cnt" type="primary" style="height: 50px" value="submit" @click="onsubmit" >Submit</a-button> 
            
    </form>
     
    </div>
</div>
    
</template>

<script>
import Antd from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css';
import Vue from 'vue';
Vue.use(Antd);


export default {
    name: 'searchw',
    components:{
        
    },
     beforeCreate () {
    this.form = this.$form.createForm(this);
  },
    data(){
        return{
            text:''
        }
    },
    methods:{
        onsubmit(){
             this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values);
          const para=this.text;
            this.$emit('search-weather', para);
            this.text="";
        }
      });
        /*    const para=this.text;
            this.$emit('search-weather', para);
            this.text="";
            */
        }
    }
}
</script>

<style  scoped>


.search-cnt{
display: flex;
flex-direction: column;
align-items: center;
flex-wrap: wrap;
align-content: center;
}
.inner-cnt{
    margin-top: 200px;
    margin-right:100px
}

.form-cnt{
    display: flex;
    flex-direction: row;
    align-content: center;
}



.btn-cnt{
    margin-left: 10px;
}



</style>


</style>
