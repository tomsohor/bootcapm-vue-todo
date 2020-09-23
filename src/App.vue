<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          v-model="query"
          class="search-bar"
          placeholder="Search....."
          @keypress="fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
          <div class="weather-box">
            <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
            <div class="weather">{{weather.weather[0].main}}</div>
          </div>
        </div>
        <video src="./assets/video.mp4" autoplay muted loop></video>
      </div>
      <div class="welcome" v-else style="margin-top:50px">
        <div class="welcome-box">Welcome to My simple vue Weather app</div>
        <video src="./assets/video.mp4" autoplay muted loop></video>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "b7c51a707a33edd61494a059f9944362",
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(res) {
      this.weather = res;
      console.log(this.weather);
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
      return `${day} ${date} ${month} ${year}`;
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
body {
  font-family: monospace, sans-serif;
  background: black;
}
/* #app {
  background-image: url("./assets/bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
} */
/* #app.warm {
  background-image: url("./assets/moon.jpg");
} */
video {
  padding: 25px;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
}
main {
  min-height: 100vh;
  padding: 60px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);

  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  margin: 20px 0;
  color: #fff;
  font-size: 70px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 30px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
  margin: 30px 0;
}
.weather-box {
  align-items: center;
  display: flex;
  justify-content: space-around;
  flex-direction: column;
}
.weather-box .temp {
  max-width: 600px;
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  margin: 20px 0;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  margin: 20px 0;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.welcome .welcome-box {
  width: 100%;
  text-align: center;
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 60px;
  font-weight: 900;
  margin: 20px 0;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
