<template>
<div>
        <v-container pt-5 class="search-cnt">
            <v-layout column >
                <v-flex>
                    <h1 class="headline">Weather Forcast</h1>
                    <h3 class="subheading grey--text">Enter the city name you want us to forecast</h3>
                </v-flex>
                <v-layout row >
                <v-flex xs6 md6>
                    <v-form
                        v-model="valid" 
                        ref="form"
                        @submit.prevent='onsubmit'>
                    <v-text-field
                        id="searchTextField"
                        class="input-cnt"
                        single-line
                        outline
                        shape
                        size=50
                        v-model="text"
                        style="height: 50px"
                        required
                    ></v-text-field>
                    </v-form>
                </v-flex>
                     <v-flex xs4 md6>
                    <v-btn 
                        class="white--text"
                        normal
                        :disabled="!valid" 
                        style="height: 45px"  
                        color="#4caf50"
                        @click="onsubmit"
                    >Submit</v-btn>
                    </v-flex>
                 
                </v-layout>
    
            </v-layout>
        </v-container>
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
    data(){
        return{
            valid: true,
            text:'',
            nameRules: [
        v => !!v || 'Name is required',
      ],
      loc_data:[{
          longitude:'',
          latitude:'',
          addr:''
      }
      ]
        }
    },
    methods:{
        onsubmit(){
      if (this.$refs.form.validate()) {
            this.$emit('search-weather', this.loc_data);
            this.$refs.form.resetValidation()
            this.text="";
        }
        },
    },
    //autocomplete function
    mounted: function () {
  var input = document.getElementById('searchTextField');
   var options = {
  	types: ['geocode'],
  };
  const place = new google.maps.places.Autocomplete(
    input, options
  );
  place.addListener('place_changed', ()=>{
      const loc=place.getPlace()
      this.loc_data.addr=loc.formatted_address;
      this.loc_data.latitude=loc.geometry.location.lat();
      this.loc_data.longitude= loc.geometry.location.lng();
  });
  
},

}
</script>

<style  scoped>


.search-cnt{
display: flex;
align-content: center;
margin-top: 150px
}
.inner-cnt{
    margin-top: 200px;
    margin-right:100px
}
/*
.form-cnt{
    display: flex;
    flex-direction: row;
    align-content: center;
}



/*.btn-cnt{
    margin-left: 10px;
}

.input-cnt{
    margin-right: 10px;
}
*/

</style>



