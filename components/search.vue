<template>
<v-app>
<div class="search-cnt">
    <div class="inner-cnt">
   <h1>Weather Forcast</h1>
   <h3>Enter the city name you want us to forecast</h3>
       <form   @submit.prevent='onsubmit'>  
              </form>
              <v-form
               v-model="valid" 
               ref="form"
               @submit.prevent='onsubmit'>

          <v-text-field
                class="input-cnt"
                label="Enter City..."
                single-line
                outline
                v-model="text"
                style="height: 50px"
                required
                :rules="nameRules"
          ></v-text-field>

        <v-btn  
            :disabled="!valid" 
            class="btn-cnt" 
            style="height: 50px"  
            color="primary"
            @click="onsubmit"
            >Submit</v-btn>
              </v-form>
     
     
     
      <a-button class="btn-cnt" type="primary" style="height: 50px" value="submit" @click="onsubmit" >Submit</a-button> 
   <a-input
          size="large" v-model="text" 
           style="height: 50px"
            placeholder="Enter City..."/>
        
    </div>
    
</div>
    </v-app>
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
    data(){
        return{
            valid: true,
            text:'',
            nameRules: [
        v => !!v || 'Name is required',
      ],
        }
    },
    methods:{
        onsubmit(){
      if (this.$refs.form.validate()) {
           const para=this.text;
            this.$emit('search-weather', para);
            this.$refs.form.resetValidation()
            this.text="";
        }
         
      
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

.input-cnt{
    margin-right: 10px;
}

</style>


</style>
