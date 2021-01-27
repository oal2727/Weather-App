<template>
  <div id="app">
    <p class="titleApp">Weather App</p>
    <CardWeather :initialWeather="initialWeather"></CardWeather>
    <CardForest :forecast="forecast"/>
  </div>
</template>

<script>
import CardWeather from './components/CardWeather/CardWeather.vue'
import CardForest from "./components/CardForest/CardForest"
export default {
  name: 'App',
  components: {
    CardWeather,
    CardForest
  },
  data(){
    return{
      ubicacion:{latitude:"",longitude:""},
      intervals:[],
      initialWeather:{},
      forecast:[]
    }
  },
  methods:{
    getPosition(){
     navigator.geolocation.getCurrentPosition(
     position => {
        const {latitude,longitude} = position.coords
       this.ubicacion.latitude=latitude
       this.ubicacion.longitude=longitude
     },
     error => {
       console.log(error.message);
     },
    )
  },
  getWeather(){
  const url =`https://api.openweathermap.org/data/2.5/weather?lat=-12.173312&lon=-76.98513919999999&exclude=hourly,daily&appid=${process.env.VUE_APP_KEY}&units=metric`
  fetch(url).
   then(response => 
    response.json()).then(data => {
       const sunset = new Date(data.sys.sunset * 1000).toLocaleTimeString().slice(0, 5);
      const sunrise = new Date(data.sys.sunrise * 1000).toLocaleTimeString().slice(0, 5);
      const param ={
        temperature:data.main.temp,
        temperature_max:data.main.temp_max,
        temperature_min:data.main.temp_min,
        description:data.weather[0].description,
        wind_speed:data.wind.speed,
        humidity:data.main.humidity,
        icon:data.weather[0].icon,
        sunrise:sunrise,
        sunset:sunset,
        main:data.weather[0].main
      }
      this.initialWeather=param
    })
  },
  
  getWeatherForecast(){
    const url =`https://api.openweathermap.org/data/2.5/forecast?lat=-12.173312&lon=-76.98513919999999&exclude=hourly,daily&appid=${process.env.VUE_APP_KEY}&units=metric`
    fetch(url).
    then(response => 
      response.json()).then(data => {
        const arrayData = data.list.slice(0,8);
        for(var i=0;i<arrayData.length;i++){
            var param ={
            temperature:arrayData[i].main.temp,
            icon:arrayData[i].weather[0].icon,
            time:arrayData[i].dt_txt,
            main:arrayData[i].weather[0].main
      
          }
          this.forecast.push(param)
        }
      })
    }
  },
  created(){
    this.getPosition();
    this.getWeather();
    this.getWeatherForecast();
   }
}
</script>

<style>
#app{
  margin-top:50px;
}
.titleApp{
   font-size: 50px;
   text-align: center;
  background: -webkit-linear-gradient(#B2E1B7, #C4C4C4);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-family: sans-serif;
}
body {
  margin: 0;
  padding: 0;
  background: #151515;
}
</style>
