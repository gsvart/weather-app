<template>
  <div id="app">
    <main class="main-wrap warm">
      <div class="search">
        <input 
          type="text" 
          class="search__input" 
          placeholder="Введите место"
          v-model="query"
          @keypress="fetchWeather"
        >
      </div>

      <div class="weather" v-if="typeof weather.main != 'undefined'">
        <div class="location">
          <div class="location__name">{{ weather.name }}</div>
        </div>

        <div class="data">
          <div class="data__temperature">{{ Math.round(weather.main.temp) }}</div>
          <div class="data__weather-type">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      url: 'https://api.openweathermap.org/data/2.5/',
      api_key: 'd92217d7025b863a72e966fbdad7cd64',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) {
      if (e.key == 'Enter') {
        fetch(`${this.url}weather?q=${this.query}&units=metric&appid=${this.api_key}&lang=RU`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
      console.log(this.weather);
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,700;1,900&display=swap');

* {
  box-sizing: border-box;
}

html {
  height: 100%;
  font-size: 16px;
  font-family: 'Roboto', sans-serif;
}

body {
  height: 100%;
  margin: 0;
  padding: 0;
}

#app {
  height: 100%;
}

main {
  padding: 2rem 1rem;
  background: rgb(0,43,142);
  background: linear-gradient(190deg, rgba(0,43,142,1) 0%, rgba(130,234,255,1) 100%);
  height: 100%;
}

main.warm {
  background: rgb(255,113,113);
  background: linear-gradient(10deg, rgba(255,113,113,1) 50%, rgba(255,243,148,1) 100%);
}

.search {
  max-width: 288px;
  margin: 0 auto 1rem;
}

.search__input {
  display: block;
  width: 100%;
  appearance: none;
  outline: none;
  border: none;
  padding: 0 1rem;
  height: 3rem;
  line-height: 100%;
  font-size: 1rem;
  border-radius: .5rem;
  color: #9e9e9e;
  box-shadow: 3px 3px 5px 0 rgba(0,0,0,.1);
}

.weather {
  max-width: 288px;
  margin: 0 auto;
  color: #fff;
  text-align: center;
  text-shadow: 3px 3px 2px rgba(0,0,0,0.1);
}

.location {
  margin-bottom: 1rem;
}

.location__name {
  font-size: 2rem;
}

.location__date {
  font-size: 1rem;
}

.data__temperature {
  font-size: 8rem;
  font-weight: 900;
  line-height: 0.9;
}

.data__weather-type {
  font-size: 1rem;
}
</style>
