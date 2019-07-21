<template>
  <div class="parent">
  
     <a-row>
      <a-col :span="12">
<searchw v-on:search-weather="getweather" />
      </a-col>
      <a-col :span="12">
          <Result
    :weather="weather" 
    :temp="temperature"
    :icon="icon"
    />
    
      </a-col>
    </a-row>
    </div>
</template>

<script>
import axios from 'axios';
import Result from '../components/result';
import searchw from '../components/search';
import Antd from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css';
import Vue from 'vue';
import { Button } from 'ant-design-vue';
import { Input} from 'ant-design-vue';
Vue.use(Antd);


export default {
  components:{
    Result,
    searchw,
    
  },
  methods:{

  async  getweather(text){
    console.log(text)
        const key="891a7691bf444406842494eb9b71b78c";
  try {
    const res = await axios.get(`http://api.openweathermap.org/data/2.5/weather?q=${text}&APPID=${key}`);
    console.log(res.data);
    this.weather= res.data.weather[0].description;
    this.temperature= res.data.main.temp;
    this.icon=res.data.weather[0].id;
    console.log(this.icon);
    console.log(this.temperature);
    
  } catch (error) {
    console.log(error)
  }
    }
  },

  data(){
    return{
      weather:" ",
      location:[
        {

        }
      ],
      icon:200,
      temperature: "",
      query:""
    }
  },



}
</script >

<style scoped>

.parent{
  height: 100vh;
}


</style>
