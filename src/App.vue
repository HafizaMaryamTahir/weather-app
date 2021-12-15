


<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          v-on:keyup.enter="submitInput"
          v-model="inputCity"
          placeholder="Search...."
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }} , {{ weather.sys.country }}
          </div>

          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.feels_like) }}°C</div>

          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

 <script>
import vue from "vue";

import axios from "axios";

import VueAxios from "vue-axios";

vue.use(VueAxios, axios);

export default {
  name: "app",
  data() {
    return {
      weather: {},
      inputCity: null,
      apiKey: "2c74fe4f73b0252351d37fd80234293b",
    };
  },
  mounted() {
    vue.axios
      .get(
        `https://api.openweathermap.org/data/2.5/weather?q=pakistan&appid=2c74fe4f73b0252351d37fd80234293b`
      )
      .then((resp) => {
         this.weather = resp.data;
        console.log(resp.data);
      });
  },
  methods: {
    //weather api data fetching method
    submitInput: function () {
      vue.axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.inputCity}&appid=2c74fe4f73b0252351d37fd80234293b`
        )
        .then((resp) => {
          this.weather = resp.data;
          console.log(resp.data);
        });
        
    },dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  },
};
</script>
  <style >
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
#app {
  background-image: url("./assets/background.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
main {
  min-height: 100vh;
  padding: 25px;
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 30%;
  padding: 15px;
  color: black;
  font-size: 20px;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 40px;
  transition: 0.4s;
  border: none;
  margin-left: 35%;
}
.search-box,
.search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgpa(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 25px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
  margin-top: 23px;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 60px;
  font-weight: 900;
  text-shadow: 3px 6px  rgb(179 197 249);
  background-color: rgb(179 197 249);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px  rgb(179 197 249);
}
.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 600;
  font-style: italic;
  background-color: rgb(179 197 249);
  border-radius: 16px;
  padding: 10px 25px;
  width: 14%;
  margin-left: 45%;
}
</style>