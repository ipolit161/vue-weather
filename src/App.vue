<template>
  <div id="App">
    <main>
      <div class="seach-box">
        <input 
        type="text " 
        class="search-bar" 
        placeholder='Search...'
        v-model="query"
        @keyup.enter="fethcWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name}}, {{weather.sys.country}}</div>
          <div class="date">Friday 7 May 2021</div>
        </div>
        <div class="weather-box">
          <div class="temp">22	&ordm;C</div>
          <div class="weather">Rain</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '534ec6ce8d1ecee22750acea98ad469a',
      url_base: 'api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fethcWeather (e) {
        console.log(e.key)
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
    },
    setResults (results) {
      this.weather = results;
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'monserrat', sans-serif;

}

#App {
  background-image: url('./assets/cold-bg.jpg');
  background-size:cover;
  background-position: bottom;
  transition: .4s;
}

main {
  min-height: 100vh;
  padding: 25px;

background-image: linear-gradient(to bottom, rgba(0,0,0, 0.25), rgba(0,0,0, 0.75));
}

.seach-box {
  width: 100%;
  margin-bottom: 30px;
}

.seach-box .search-bar {
  display: block;
  width: 100%;
  padding:15px;
  color: #313131;
  font-size: 20px;

  appearance: none;
  border:none;
  outline:none;
  background: none;

box-shadow: 0 0 16px rgba(0,0,0, 0.25);
  background-color: rgba(255, 255, 255, .5);
  border-radius: 0 16px 0 16px;
  transition:.4s;

}

.seach-box .search-bar:focus{
  box-shadow:rgba(0,0,0, 0.25);
  background-color: rgba(255, 255, 255, .75);
  border-radius: 16px 0 16px 0;
}

.location-box .location {
  color:#fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0, 0.25);
}

.location-box .date{
    color:#fff;
    font-size: 20px;
    font-weight: 300;
    font-style: italic;
    text-align: center;
}

.weather-box{
  text-align: center;
}
.weather-box .temp{
  display: inline-block;
  padding: 10px 20px;
  color: #fff;
  font-size: 102px;
  font-weight:900;

  text-shadow: 3px 6px rgba(0,0,0, 0.25);
  background: rgba(255, 255, 255, .25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0,0,0, 0.25);
}

.weather-box .weather{
  color:#fff;
  font-size: 48px;
  font-style: italic;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0,0,0, 0.25);
}
</style>
