<template>
  <div class="hello">
    <div class="title">
      <div class="top"><input type="text" placeholder="Puri" v-model="query" @keypress="fetchwea"></div>
      <div class="tame"> {{ this.min }} : {{ this.sec }} </div>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Clouds' && this.time==true">
      <img src="../assets/2682849_cloud_cloudy_day_forecast_sun_icon.svg" alt="" class="img"><br>
      <label >Cloudy</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Clouds' && this.time==false">
      <img src="../assets/2682846_cloud_cloudy_forecast_moon_night_icon.svg" alt="" class="img"><br>
      <label >Cloudy</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Thunderstorm'">
      <img src="../assets/118967_weather_storm_icon.svg" alt="" class="img"><br>
      <label>Thunderstrom</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Clear' && this.time==true">
      <img src="../assets/2682802_cloudy_day_fog_foggy_mist_icon.svg" alt="" class="img"><br>
      <label>Clear</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Clear' && this.time==false">
      <img src="../assets/2682847_eclipse_forecast_moon_night_space_icon.svg" alt="" class="img"><br>
      <label>Clear</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Snow'">
      <img src="../assets/2682816_cloud_cloudy_forecast_precipitation_snow_icon.svg" alt="" class="img"><br>
      <label>Snow</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Rain'">
      <img src="../assets/2682845_cloud_cloudy_forecast_rain_sun_icon.svg" alt="" class="img"><br>
      <label>Rain</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Mist'">
      <img src="../assets/2682838_cloud_cloudy_drop_forecast_rain_icon.svg" alt="" class="img"><br>
      <label>Mist</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Smoke'">
      <img src="../assets/2682805_acid_carbon_co2_dioxide_mist_icon.svg" alt="" class="img"><br>
      <label>Smoke</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Haze'">
      <img src="../assets/2682841_cloud_cloudy_forecast_storm_weather_icon.svg" alt="" class="img"><br>
      <label>Haze</label>
    </div>
    <div class="image" v-if="weather.weather[0].main=='Fog'">
      <img src="../assets/2682841_cloud_cloudy_forecast_storm_weather_icon.svg" alt="" class="img"><br>
      <label>Fog</label>
    </div>

    <div class="image" v-if="weather.weather[0].main=='Storm'">
      <img src="../assets/118967_weather_storm_icon.svg" alt="" class="img"><br>
      <label>Storm</label>
    </div><div class="image" v-if="weather.main=='Windy'">
      <img src="../assets/118967_weather_storm_icon.svg" alt="" class="img"><br>
      <label>Windy</label>
    </div>
    <div class="image" v-if="weather.main=='Hail'">
      <img src="../assets/118967_weather_storm_icon.svg" alt="" class="img"><br>
      <label>Hail</label>
    </div>

    <div class="info">
      <br>
      <div class="info2">
        <div class="wind">
          <img src="../assets/2682842_breeze_fast_speed_weather_wind_icon.svg" alt="" class="img2">
          
        </div>
        <div class="hum">
          <img src="../assets/2682807_drop_high_humidity_percentage_precipitation_icon.svg" alt="" class="img2">
          
        </div>
        <div class="sun">
          <img src="../assets/2682808_high_hot_summer_temperature_termometer_icon.svg" alt="" class="img2">
          
        </div>
      </div>
      <div style="justify-content: space-between;display: flex;width: 85%">
        <div class="dat">
        <span class="lab">{{ weather.wind.speed }} km/h</span><br><br>
        <span class="lab">{{ weather.main.humidity }}%</span><br><br>
        <span class="lab">{{ weather.main.pressure }} mbar</span>
      </div>
      <div class="temp">
        <br>
        <br>
        <span>{{ Math.round(weather.main.temp) }}<sup>&#176;</sup></span>
      </div>
      </div>
      
    </div>
  </div>
</template>

<script>
import './div.css';
export default {
  name: 'DiviSion',
  data(){
    return{
      api_key: '68059808d9e9f4aff8772b6aad5d97a4',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: 'Puri',
      weather: {"coord":{"lon":85.85,"lat":19.8},"weather":[{"id":803,"main":"Clouds","description":"broken clouds","icon":"04d"}],"base":"stations","main":{"temp":27.29,"feels_like":30.4,"temp_min":27.29,"temp_max":27.29,"pressure":1014,"humidity":80,"sea_level":1014,"grnd_level":1014},"visibility":10000,"wind":{"speed":7.27,"deg":207,"gust":9.25},"clouds":{"all":72},"dt":1649123537,"sys":{"type":1,"id":9113,"country":"IN","sunrise":1649117222,"sunset":1649161883},"timezone":19800,"id":1259184,"name":"Puri","cod":200},
      time: 'false',
      sec: '',
      min:''
    }
  },
  created () {
    fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(res=>{
          return res.json();
        }).then(this.setResults);

    const dom = new Date();
    this.sec= dom.getMinutes();
    this.min= dom.getHours();
  },
  methods:{
    fetchwea(e){
      if(e.key=="Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(res=>{
          return res.json();
        }).then(this.setResults);
        }
        this.value="";
      },
      setResults(results){
        this.weather = results;
        let ti = this.weather.weather[0].icon;
        if(ti.includes("n")){
          this.time=false;
        }
        else{
          this.time=true;
        }
      },
  }
}
</script>
<style scoped>
.hello{

}
</style>
