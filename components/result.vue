<template>
    <div  class="display-cnt">
      <v-container  >
        <v-layout ml-5 column>
          <v-flex >
            <canvas id="icon2" width="250" height="250"></canvas>
          </v-flex>
          <v-flex>
             <h1 class="white--text">
          {{weather}}
        </h1>
          </v-flex>
          <v-flex >
             <h1 class="white--text">
          {{temp}} 
        </h1>
          </v-flex>
          <v-flex >
               <h2 class="white--text">
             {{addr}}
          </h2>
          </v-flex>
        </v-layout>
        
       
       
     
        <h1>
          {{humidity}}
        </h1>
      </v-container>
    </div>
</template>

<script>
  


export default {
    name: 'Result',
    props: ['temp' , 'weather', 'icon', 'addr', 'humidity', ],
    computed:{
         humidity(){
              const skycons = new Skycons({"color": "#f5f5f5"});
              skycons.add(document.getElementById('icon2'), Skycons[this.icon]);
              return  skycons.play();
            
          },  
 
}
}

</script>



<style scoped>
.display-cnt{
display: flex;
flex-direction: column;
background-color: #4caf50;
align-items: center;
flex-wrap: wrap;
align-content: center;

min-height: 100vh;
}
.inner-cnt{
    margin-top: 50%;
}

.img-cnt{
    /*background: crimson; */
    height: 300px;
    margin-top: 80px;
}

</style>
