<template>
  
  <div id="main" :class="isDay ? 'day' : 'night'">
      <div class="container my-5" style="max-width: 650px; min-width: 650px">
        <h1 class="title text-center">Weather App </h1>
        <form class="search-location" v-on:submit.prevent="getWeather" >
          <input  
            type="text"
            class="form-control text-muted form-rounded p-3 shadow-sm"
            placeholder="Wich City?"
            v-model="citySearch"
            autocomplete="off"
            @keypress="getForecast"
          />
        </form>

      <div
        class="card rounded my-3 shadow-lg back-card overflow-hidden"
        v-if="visible"
      >
      <div class="rain" v-if="rain">
          <span style="--i:11"> </span>
          <span style="--i:12"> </span>
          <span style="--i:10"> </span>
          <span style="--i:14"> </span> 
          <span style="--i:18"> </span>
          <span style="--i:16"> </span>
          <span style="--i:19"> </span>
          <span style="--i:10"> </span>
          <span style="--i:16"> </span>
          <span style="--i:16"> </span>
          <span style="--i:19"> </span>
          <span style="--i:10"> </span>
          <span style="--i:16"> </span>
          <span style="--i:19"> </span>
          <span style="--i:10"> </span>
          <span style="--i:13"> </span>
          <span style="--i:12"> </span>
          <span style="--i:15"> </span>
          <span style="--i:10"> </span>
          <span style="--i:10"> </span>
          <span style="--i:14"> </span>
          <span style="--i:18"> </span>
          <span style="--i:15"> </span>
          <span style="--i:16"> </span>
          <span style="--i:15"> </span>
          <span style="--i:10"> </span>
          <span style="--i:16"> </span>
        </div>
        <div class="snow" v-if="snow">
          <span style="--a:13"> </span>
          <span style="--a:12"> </span>
          <span style="--a:10"> </span>
          <span style="--a:14"> </span>
          <span style="--a:18"> </span>
          <span style="--a:16"> </span>
          <span style="--a:19"> </span>
          <span style="--a:10"> </span>
          <span style="--a:16"> </span>
          <span style="--a:16"> </span>
          <span style="--a:19"> </span>
          <span style="--a:10"> </span>
          <span style="--a:16"> </span>
        </div>
        <span class="cloud" v-if="cloud">
          <span  style="--b:15" ></span>
          <span  style="--b:12" ></span>
          <span  style="--b:10" ></span>
          <span  style="--b:17" ></span>
          <span  style="--b:18" ></span>
          <span  style="--b:19" ></span>
        </span>
        <span class="sun" v-if="sun">
          <span>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
          </span>
        </span>
        <div>
          </div>
          <div class="card-body text-center" style="margin-bottom: 15rem">
          <div class="city-name my-3">
            <div class="today">{{ dateBuilder() }}</div>
              <div class="card-bottom">{{ weather.cityName }},{{ weather.country }}</div>
              <div style="font-size: 30px; font-style: oblique; "> {{ weather.temperature }}&deg;C 
              <img  :src='require(`../static/${weather.icon}.png`)' alt="" class="img_main"></div>
              <div class="weather-name" >{{ weather.main }} </div>
            <div class="info" >
              <div>   <p style="font-size:15px">Humidity</p> 
                <droplet-icon size="1.5x" class="custom-class"></droplet-icon> 
                {{ weather.humidity }}%
              </div>
              <div> 
                <p style="font-size:15px">Wind Speed</p>
                <wind-icon size="1.5x" class="custom-class"></wind-icon>
                {{ weather.speed }}</div>
              <div>  
                <p style="font-size:15px">Clouds</p>
                <cloud-icon size="1.5x" class="custom-class"></cloud-icon> 
                %{{ weather.clouds }}</div>
      
          </div>
          </div>
        </div>
        <p class="days5" >--------------------------------- 5-Days Forecast ----------------------------------</p>
        <div class="daily">
            <div class="day1">
              Day 1
              <img :src='require(`../static/${forecast.icon1}.png`)' alt="" class="img"  > 
              <p>   <thermometer-icon size="1.5x" class="custom-class"></thermometer-icon> {{ forecast.temp1}} &deg;C</p>
              <p> <droplet-icon size="1.5x" class="custom-class"></droplet-icon> {{ forecast.hum1 }}%</p>
              <p> <wind-icon size="1.5x" class="custom-class"></wind-icon> {{ forecast.speed1 }}</p>
            </div>
            <div class="day2">
              Day 2 
              <img :src='require(`../static/${forecast.icon2}.png`)' alt="" class="img">
              <p>   <thermometer-icon size="1.5x" class="custom-class"></thermometer-icon> {{ forecast.temp2}}  &deg;C</p>
              <p> <droplet-icon size="1.5x" class="custom-class"></droplet-icon> {{ forecast.hum2 }}%</p>
              <p> <wind-icon size="1.5x" class="custom-class"></wind-icon> {{ forecast.speed2 }}</p>
            </div>
            <div class="day3">
              Day 3
              <img :src='require(`../static/${forecast.icon3}.png`)' alt="" class="img">
             <p>    <thermometer-icon size="1.5x" class="custom-class"></thermometer-icon> {{ forecast.temp3}} &deg;C</p>
              <p> <droplet-icon size="1.5x" class="custom-class"></droplet-icon>{{ forecast.hum3 }}%</p>
              <p> <wind-icon size="1.5x" class="custom-class"></wind-icon> {{ forecast.speed3 }}</p>
            </div>
            <div class="day4">
              Day 4 
              <img :src='require(`../static/${forecast.icon4}.png`)' alt="" class="img">
             <p>   <thermometer-icon size="1.5x" class="custom-class"></thermometer-icon> {{ forecast.temp4}} &deg;C</p>
              <p> <droplet-icon size="1.5x" class="custom-class"></droplet-icon>{{ forecast.hum4 }}%</p>
              <p> <wind-icon size="1.5x" class="custom-class"></wind-icon> {{ forecast.speed4 }}</p>
            </div>
            <div class="day5">
              Day 5 
              <img :src='require(`../static/${forecast.icon5}.png`)' alt="" class="img">
              <p>   <thermometer-icon size="1.5x" class="custom-class"></thermometer-icon> {{ forecast.temp5}} &deg;C</p>
              <p> <droplet-icon size="1.5x" class="custom-class"></droplet-icon>{{ forecast.hum5 }}%</p>
              <p> <wind-icon size="1.5x" class="custom-class"></wind-icon> {{ forecast.speed5 }}</p>
            </div>
        </div>
        </div>
      </div>
    </div>
</template>

<script>
import {  WindIcon, DropletIcon, CloudIcon, ThermometerIcon } from "vue-feather-icons";
 export default {
  components: {
    WindIcon,
    DropletIcon,
    ThermometerIcon,
    CloudIcon
  },
  data() {
    return {
      visible: false,
      rain: false,
      cloud: false,
      sun: false,
      snow: false,
      isDay: true,
      citySearch: "",
      weather: {
        cityName: "",
        country: "",
        temperature: 0,
        description: "",
        humidity: "",
        icon:"",
        speed:"",
        clouds:""
      },
      forecast:{
        icon1:"",
        temp1:0,
        hum1:0,
        speed1:0,
        icon2:"",
        temp2:0,
        hum2:0,
        speed2:0,
        icon3:"",
        temp3:0,
        hum3:0,
        speed3:0,
        icon4:"",
        temp4:0,
        hum4:0,
        speed4:0,
        icon5:"",
        temp5:0,
        hum5:0,
        speed5:0
      }
    };
  },
  methods: {
    getWeather: async function () {
      console.log(this.citySearch);
      const key = "3c7eaf1e85a8ed2065fb086c51056e84";
      const baseURL = `https://api.openweathermap.org/data/2.5/weather?q=${this.citySearch}&appid=${key}&units=metric`;
      
      try {
        const response = await fetch(baseURL);
        const data = await response.json();
        console.log(data);
        this.citySearch = "";
        this.weather.cityName = data.name;
        this.weather.country = data.sys.country;
        this.weather.temperature = Math.round(data.main.temp);
        this.weather.main = data.weather[0].main;
        this.weather.humidity = Math.round(data.main.humidity);
        this.weather.clouds = data.clouds.all;
        this.weather.icon = data.weather[0].icon;
        this.weather.speed = data.wind.speed;
        const timeOfDay = data.weather[0].icon;
        if (timeOfDay.includes("n")) {
          this.isDay = false;
        } else {
          this.isDay = true;
        }
        this.visible = true;
      } catch (error) {
        this.visible = false;
      }
      
      if (this.weather.main==("Rain")) {
          this.cloud = false;
          this.rain = true;
          this.sun = false;
          this.snowy = false;
        }
        if (this.weather.main==("Snow")) {
          this.cloud = false;
          this.rain = false;
          this.sun = false;
          this.snow = true;
        }
        if (this.weather.main==("Clouds")) {
          this.rain = false;
          this.snow = false;
          this.cloud = true;
          this.sun = false;
        }
        if (this.weather.main==("Clear")) {
          this.rain = false;
          this.snow = false;
          this.cloud = false;
          this.sun = true;
        }
    },
    getForecast: async function () {
      console.log(this.citySearch);
      const key = "3c7eaf1e85a8ed2065fb086c51056e84";
      const baseURL = `https://api.openweathermap.org/data/2.5/forecast?q=${this.citySearch}&appid=${key}&units=metric`;
      try {
        const response = await fetch(baseURL);
        const data = await response.json();
        this.forecast.temp1 = Math.round(data.list[0].main.temp);
        this.forecast.hum1=Math.round(data.list[0].main.humidity);
        this.forecast.speed1 = data.list[0].wind.speed;
        this.forecast.icon1= data.list[0].weather[0].icon;
        this.forecast.temp2 = Math.round(data.list[1].main.temp);
        this.forecast.hum2=Math.round(data.list[1].main.humidity);
        this.forecast.speed2 = data.list[1].wind.speed;
        this.forecast.icon2= data.list[1].weather[0].icon;
        this.forecast.temp3 = Math.round(data.list[2].main.temp);
        this.forecast.hum3=Math.round(data.list[2].main.humidity);
        this.forecast.speed3 = data.list[2].wind.speed;
        this.forecast.icon3= data.list[2].weather[0].icon;
        this.forecast.temp4 = Math.round(data.list[3].main.temp);
        this.forecast.hum4=Math.round(data.list[3].main.humidity);
        this.forecast.speed4 =data.list[3].wind.speed;
        this.forecast.icon4= data.list[3].weather[0].icon;
        this.forecast.temp5 = Math.round(data.list[4].main.temp);
        this.forecast.hum5=Math.round(data.list[4].main.humidity);
        this.forecast.speed5 = data.list[4].wind.speed;
        this.forecast.icon5= data.list[4].weather[0].icon;
      }catch (error) {
        this.visible = false;
      }

    },
  dateBuilder(){
            let d = new Date();
            let months= ["January","February","March","April","May","July",
            "August","September","October","November","December"];
            let days =["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];
            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();
            return `${day}, ${date} ${month} ${year}`;
      }
  }
};

</script>
    
<style>
@import url(../store/style.css);
</style>