<template>
  <div id="app">

    <header>
      <h1>Weather App</h1>
      <p>Search your city or other ones to see what's the weather like</p>
    </header>

    <form>
      <input type="text" placeholder="Enter city name.." v-model="city"/>
    </form>

    <div class="info">
      <div class="place">Valjevo, Serbia</div>
      <div class="date">20.11.2020</div>
      <br>
      <div class="temp">10°C</div>
      <div class="weather">Rain</div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      city: ''
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
  transition: 0.5s;
}

input:focus {
  background-color: rgba(255, 255, 255, 0.8); 
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.7);
  border-radius: 0 15px;
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
