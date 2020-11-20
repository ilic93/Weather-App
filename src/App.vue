<template>
  <div id="app" :class="`${changeBackground()}`">

    <header>
      <h1>Weather App</h1>
      <p>Search your city or other ones to see what's the weather like</p>
    </header>

    <form>
      <input type="text" placeholder="Enter city name.." v-model="city" @keydown.enter="fetchWeather"/>
    </form>

    <div class="no-city" v-if="weather.cod == 404">
      {{ weather.message }}
    </div>

    <div class="info" v-if="typeof weather.main !== 'undefined'">
      <div class="place">{{ weather.name }}, {{ weather.sys.country }}</div>
      <div class="date">{{ fetchDate() }}</div>
      <br>
      <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
      <div class="weather">{{ weather.weather[0].main }}</div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      city: '',
      api_key: '2f05e1af6fc508a515d1265455be372f',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) {
      e.preventDefault()
      fetch(`${this.url_base}weather?q=${this.city}&units=metric&APPID=${this.api_key}`)
      .then(res => res.json())
      .then(res => {
        console.log(res)
        this.weather = res
      })
      this.city = ''
    },
    fetchDate() {
      const today = new Date()
      const months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
      const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]

      const day = days[today.getDay()]
      const date = today.getDate()
      const month = months[today.getMonth()]
      const year = today.getFullYear()

      return `${day}, ${date}.${month}, ${year}`
    },
    changeBackground() {
      if(typeof this.weather.main == 'undefined') return ''
      let weatherClass
      switch(this.weather.weather[0].main) {
        case 'Rain':
        case 'Drizzle':
          weatherClass = 'rainy'
          break
        case 'Fog':
        case 'Mist':
          weatherClass = 'foggy'
          break
        case 'Clouds':
          weatherClass = 'cloudy'
          break
        case 'Snow':
          weatherClass = 'snowy'
          break
        default:
          weatherClass = ''
      }
      console.log('hello')
      return weatherClass
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Goldman&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Goldman', cursive;
}

#app {
  text-align: center;
  background-image: url('./assets/sunny-weather.jpg');
  min-height: 100vh;
  background-size: cover;
  padding: 20px;
  transition: 0.5s;
}

#app.rainy {
  background-image: url('./assets/rain.jpg');
}

#app.foggy {
  background-image: url('./assets/fog.jpg');
}

#app.cloudy {
  background-image: url('./assets/clouds.jpg');
}

#app.snowy {
  background-image: url('./assets/snow.jpg');
}

header {
  font-size: 20px;
  margin: 20px 0;
}

input {
  width: 100%;
  font-size: 25px;
  padding: 10px;
  color: black;

  background-color: rgba(255, 255, 255, 0.5);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
  border-radius: 15px 0;
  border: none;
  outline: none;
  transition: 0.5s; /* doesn't work in Mozilla */
}

input:focus {
  background-color: rgba(255, 255, 255, 0.8); 
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.7);
  border-radius: 0 15px;
}

.no-city {
  font-size: 50px;
  margin-top: 15px;
  color: white;
  text-shadow: 5px 5px 10px rgba(0, 0, 0, 0.8)
}

.info {
  color: white;
  margin-top: 20px;
  font-size: 40px;
}

.place, .date, .temp, .weather {
  text-shadow: 2px 2px rgba(0, 0, 0, 1);
}

.date {
  font-style: italic;
  font-weight: 200;
}

.temp {
  display: inline-block;
  font-size: 90px;
  font-weight: 700;
  background-color: rgba(255, 255, 255, 0.3);
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 15px;
  box-shadow: 5px 5px rgba(0, 0, 0, 0.3);
}


</style>
