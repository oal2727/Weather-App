<template>
  <div class="weather-initial">
    <div class="weather-content">
      <div class="weather-header">
            <i id="image-weather" :class="setIcon(initialWeather.main)"></i>
        <div class="weather-column">
          <span class="weather-temperature">{{Math.round(initialWeather.temperature)}}°</span>
          <p class="weather-description">{{initialWeather.description}}</p>
        </div>
      </div>

      <div class="weather-body">
        <div class="weather-body-content">

          <div class="weather-box">
            <span class="weather-box-temperature">{{ initialWeather.temperature_min }}°</span>
            <p class="weather-box-description">High</p>
             </div>

               <div class="weather-box">
               <span class="weather-box-temperature">{{ initialWeather.wind_speed }}mph</span>
            <p class="weather-box-description">Wind Speed</p>
             </div>


               <div class="weather-box">
               <span class="weather-box-temperature">{{ initialWeather.sunrise }}</span>
            <p class="weather-box-description">Sunrise</p>
             </div>

               <div class="weather-box">
               <span class="weather-box-temperature">{{ initialWeather.temperature_max }}°</span>
            <p class="weather-box-description">Low</p>
                </div>

                 <div class="weather-box">
               <span class="weather-box-temperature">{{ initialWeather.humidity }}%</span>
            <p class="weather-box-description">Humidity</p>
             </div>

                 <div class="weather-box">
               <span class="weather-box-temperature">{{ initialWeather.sunset }}</span>
            <p class="weather-box-description">Sunset</p>
            </div>

        </div>
      </div>
    </div>

  </div>
</template>
<script>
import "./style.css"
export default {
  props:["initialWeather"],
  methods:{
    setIcon(icon){
      if(icon === "Clear"){
        return "fas fa-cloud-sun"
      }else if(icon === "Thunderstorm"){
        return "fad fa-thuderstorm"
      }else if(icon === "Rain"){
        return "fas fa-cloud-showers-heavy"
      }else if(icon === "Snow"){
        return "fas fa-snowflake"
      }else if(icon === "Clouds"){
        return "fas fa-cloud"
      }else if(icon === "Drizzle"){
        return "fas fa-cloud-drizzle"
      }else{
        return "fas fa-smog"
      }
    },
  },
  
};
</script>
