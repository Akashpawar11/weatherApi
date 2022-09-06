<template>
  <div id="app" class="container-fluid">
    <main>

      <div class="search-box row pt-4">
        <div class="col-12 search-bar">
          <input type="text" v-model="query" @keypress="fetchQuery" class=" searchBar col-6 offset-3 py-1" placeholder="Search...">
        </div>
      </div>

      <div class="weather-wrap row pt-4" v-if="typeof weather.main != undefined">
        <div class="location-box col-6 offset-3 text-center">
          <div class="location">{{ this.weather.name }}</div>
          <div class="date ">06/09/2022</div>
        </div>

        <div class="temp-box col-6 offset-3 text-center pt-4">
          <div class="temp py-2 px-2 md-2">{{ Math.round(temp)}}℃</div>
          <div class="weather">{{this.weatherCondition}}</div>
        </div>
      </div>
    </main>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      api_key: '61da71aa805bc64ddb67d0f48c4a2922',
      base_url: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: '',
      weatherCondition: '',
      temp: ''

    }
  },
  methods: {
   async fetchQuery(e) {
      if (e.key == 'Enter') {
        let results = await axios.get(`${this.base_url}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
        //     .then(res => {
        //       return res.json();
        //     }).then(this.setResults);
        this.temp = results.data.main.temp
        this.weatherCondition = results.data.weather[0].main
        this.weather = results.data;
        // console.log("APIDATA",results.data);
        // console.log("APIDATA",results.data.weather[0].main);
        console.log("APIDATA",results.data.weather[0].main);
        // }
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

}

body {
  /* background-image: url(./assets/clouds.jpg); */
  background-color: rgb(16, 54, 60);
  background-size: cover;
  font-family: 'monteserrat', sans-serif;
  transition: 0.5s;
}

.searchBar {
  background-color: rgba(255, 255, 255, 0.66);
  border: none;
  outline: none;
  border-radius: 0 10px 0 10px;
}

.searchBar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  border: none;
  outline: none;
  border-radius: 10px 0 10px 0;
  transition: 0.4s;
}

.location {
  color: antiquewhite;
  font-size: 45px;
  font-weight: 800;
  text-shadow: 3px 3px rgba(0, 0, 0, 0.407);
}

.date {
  color: white;
  font-size: 25px;
  font-weight: 500;
  text-shadow: 3px 1px rgba(23, 23, 23, 0.3);
}

.temp {
  font-size: 70px;
  border-radius: 10px;
  font-family: 'Dosis', sans-serif;
  color: #c5c5c5;
  ;
  /* font-family: 'Fredoka One', cursive; */
  background-color: rgba(255, 255, 255, 0.35);
  /* box-shadow: 3px 6px ; */
}

.weather {
  color: #ffffff;
  font-size: 35px;
  font-family: calibri;
}
</style>
