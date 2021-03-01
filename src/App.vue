<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-2"></div>
        <div class="col-md-6">
          <h2>Weather App</h2>
            <br>
            <div class="form-group">
              <form v-on:submit.prevent="getWeather">
                <input type="text" v-model="citySearch" class="form-control" placeholder="type city name and press enter"/>
              </form>
            </div>
            <br>
            <br>
            <br>
            <br>

            <div v-if="correct == true && found == true">
              <h5>The current temperature in {{citySearch}} is: {{currentTemp}}</h5>
              <h5>And the wind's speed is: {{wind}}</h5>
              <!-- <h1>{{pressure}}</h1>
              <h1>{{overcast}}</h1> -->
            </div>
        </div>
        <div class="col-md-2"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data() {
    return {
      correct: "false",
      found: "false",
      citySearch: "",
      currentTemp: '',
      minTemp: '',
      maxTemp:'',
      sunrise: '',
      sunset: '',
      pressure: '',
      humidity: '',
      wind: '',
      overcast: '',
      icon: ''
        }
      },
      
  components: {
  },
  methods: {
    getWeather: async function () {
      console.log(this.citySearch);
      const key = "5299e83c9cf2fef510fb8ddaa3206ac8";
      const baseURL = `http://api.openweathermap.org/data/2.5/weather?q=${this.citySearch}&appid=${key}&units=metric`;

      try {
        const response = axios.get(baseURL).then(response => {
          console.log(response.data)
          this.currentTemp = response.data.main.temp;
          this.minTemp = response.data.main.temp_min;
          this.maxTemp = response.data.main.temp_max;
          this.pressure = response.data.main.pressure;
          this.humidity = response.data.main.humidity + '%';
          this.wind = response.data.wind.speed + 'm/s';
          this.correct = true;
          this.found = true;
          // console.log(response.data.name);
          // this.name = response.data.name;
          // this.overcast = response.data.weather[0].description;
          // this.icon = "images/" + response.data.weather[0].icon.slice(0, 2) + ".svg";
          // this.sunrise = new Date(response.data.sys.sunrise*1000).toLocaleTimeString("en-GB").slice(0,4);
          // this.sunset = new Date(response.data.sys.sunset*1000).toLocaleTimeString("en-GB").slice(0,4);
  })
      }catch (error){
        console.log(error);
      }
    },
  //   beforeMount() {
  //   this.getWeather();
  // }
  }
}
</script>

<style>
</style>
