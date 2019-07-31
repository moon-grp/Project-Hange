<template>
  <div >  
      <v-layout row >
        <v-flex xs12 md6>
          <searchw
          v-on:search-weather="getweather" />
        </v-flex>
        <v-flex xs12 md6 >
         <Result
          :weather="weather"
          :temp="temperature"
          :humidity="humidity"
          :icon="icon"
          :addr="addr"
          />
        </v-flex>
      </v-layout>
    



  
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
import 'vuetify/dist/vuetify.min.css';
import Vuetify from 'vuetify';
Vue.use(Vuetify);



export default {
  components:{
    Result,
    searchw,
    
  },
  methods:{

  async  getweather(text){
  try {
   const res= await axios.get(`https://cors-anywhere.herokuapp.com/https://api.darksky.net/forecast/${process.env.API_KEY}/${text.latitude},${text.longitude}?units=auto`)
    console.log(res.data.currently);
    this.weather="Forcast: " + res.data.currently.summary;
    this.temperature= "Temperature: " + res.data.currently.temperature;
    this.humidity= "Humidity: " + res.data.currently.humidity;
    this.icon=res.data.currently.icon.replace(/-/g, "_").toUpperCase();
    this.addr="Location: " + text.addr;
  } catch (error) {
    console.log(error)
  }
    },
  },

  data(){
    return{
      weather:" ",
      location:'',
      icon:'',
      temperature: "",
      humidity:""
    }
  },
  



}
</script >

<style scoped>

.parent{
  height: 100vh;
}


</style>
