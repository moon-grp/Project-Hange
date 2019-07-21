<template>
    <div  class="display-cnt">
        <img class="img-cnt" :src="require('../assets/OpenWeatherMap/' + icon + '.svg')" alt="">
        <h1>
          {{weather}}
        </h1>
        <h1>
             {{temp}}
        </h1>
        
    </div>
</template>

<script>
export default {
    name: 'Result',
    props: ['temp' , 'weather', 'icon']

}
</script>



<style scoped>
.display-cnt{
display: flex;
flex-direction: column;
border: 1px #ccc solid;
align-items: center;
flex-wrap: wrap;
align-content: center;
background: #1890ff;
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
