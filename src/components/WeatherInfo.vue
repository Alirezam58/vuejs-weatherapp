<template>
<div class="container">
<div class="inner-container">
    <!--<button @click="GetWeatherData()">Get Data</button>-->
    <h2>{{temprature}}<span>&#176;</span></h2>
    
    {{weatherDesc}}
    <div v-if="showRainy" class="weather-condition">
        <img src='../assets/weatherImg/rainy.png' />
    </div>
    <div v-if="showCloudy" class="weather-condition">
        <img src='../assets/weatherImg/cloudy.png' />
    </div>
    <div class="weather-condition">
        <img v-if="showSunny" src='../assets/weatherImg/sunny.png' />
    </div>
    
</div>
</div>
</template>

<script>
import axios from 'axios';
export default{
    data(){
        return{
            weather:{},
            weatherDesc:'',
            showCloudy:false,
            showSunny:false,
            showRainy:false,
            temprature:''
        }
    },
    methods:{
        GetWeatherData(){
            axios.get('https://api.openweathermap.org/data/2.5/weather?lat=37.272&lon=49.614&appid=67383f33230f54756140e05dd49dc6b1&units=metric')
            .then(
                response =>{
                    let mainDescription = response.data.weather[0].main;
                    this.weatherDesc = response.data.weather[0].description;
                    this.temprature = response.data.main.temp;

                    if(mainDescription =='Clouds'){
                        this.showCloudy =true;
                    }else if(mainDescription == 'Rain'){
                        this.showRainy == true;
                    }else if(mainDescription == 'Sunny'){
                        this.showSunny=true;
                    }
                }
            ).catch(
                error =>{
                    console.log(error);
                }
            )
        }
    },
    mounted(){
        this.GetWeatherData();
    }
}
</script>

<style>
.container{
    width: 100%;
    display: flex;
    align-items: center;
}

.inner-container{
    width: 50%;
    margin: 0 auto;
    background-color: #e2e2e2;
}
</style>