<template>
  <div id="app" :class="typeof weather.main != 'undefined'">
    <main>
      <div class="wrapper">
        <div class="button-wrapper">
          <div class="header">To change your life</div>
          <div class="subheader">press the button</div>
          <button @click="fetchWeather" class="button" onClick="fetchWeather">
            OKAY
          </button>
        </div>

        <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
          <div class="location-box">
            <div class="location">{{ weather.name }}, TN</div>
            <div class="date">{{ dateBuilder() }}</div>
          </div>

          <div class="weather-box">
            <div class="temp">
              {{ weather.weather[0].main }} ~
              {{ Math.round(weather.main.temp) }}°f
            </div>
          </div>

          <div>
            <div class="gift-message">Happy Christmas !</div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "app",

  data() {
    return {
      api_key: "9bfd40f5956af5b26d05e4c9350a1d4f",
      url_base: "https://api.openweathermap.org/data/2.5/",
      lon: "-86.7844",
      lat: "36.1659",
      weather: {},
    };
  },

  methods: {
    fetchWeather() {
      fetch(
        `${this.url_base}weather?lat=${this.lat}&lon=${this.lon}&units=imperial&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },

    setResults(results) {
      this.weather = results;
    },

    dateBuilder() {
      let d = new Date();

      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];

      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date}, ${month} ${year}`;
    },
  },
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

body {
  font-family: "Poppins", sans-serif;
  background-color: rgba(0, 135, 62, 0.6);
}

main {
  width: 100%;
  max-width: 1200px;
  padding: 0 20px;
}

.wrapper {
  background-color: rgba(250, 188, 2, 0.6);
  padding-right: 3rem;
  padding-left: 3rem;
  padding-top: 1rem;
  padding-bottom: 2rem;
  opacity: 0.7;
  border-radius: 15px;
}

.header {
  font-size: 40px;
  color: #d6001c;
  text-align: center;
  margin-bottom: 5px;
}

.subheader {
  font-size: 40px;
  color: #d6001c;
  text-align: center;
  margin-bottom: 20px;
}

.button-wrapper .button {
  display: block;
  width: 60%;
  padding: 30px;
  margin: 0 auto;

  color: #d6001c;
  font-size: 40px;

  border: none;
  outline: none;

  background-color: rgba(255, 255, 255, 0.6);
  border-radius: 25px 10px 25px 10px;

  margin-top: 30px;
  margin-bottom: 30px;
}

.button-wrapper .button:hover {
  background-color: rgba(255, 255, 255, 0.8);
  cursor: pointer;
}

.location-box {
  font-size: 30px;
  color: #d6001c;
  text-align: center;
  margin-bottom: 20px;
}

.weather-box {
  font-size: 40px;
  color: #d6001c;
  text-align: center;
  margin-bottom: 20px;
}

.gift-message {
  font-size: 30px;
  color: #00873e;
  text-align: center;
  font-weight: 700;
  margin-bottom: 20px;
}
</style>
