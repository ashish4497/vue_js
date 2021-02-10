<template>
  <div class="uk-container uk-container-large">
     <h1 class="uk-heading-divider">Weather</h1>
    <div class="search_bar uk-margin">
      <input type="text" class="uk-input" placeholder="Search.." v-model="inputvalue" @keypress="fetchdata"/> 
    </div>
   <div class="weather_description">
     <h1 class="uk-heading-small">{{weather.name}}</h1>
     <span> {{`${weather.main.temp} Temp`}}</span>
      <p> {{`${weather.wind.speed} wind speed `}}</p>         
   </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      weather_key :"6d5040a41d57589ede9e9d053683de79",
      api_url :"https://api.openweathermap.org/data/2.5/",
      inputvalue : "",
      weather:{}
    }
  },

  methods : {
    fetchdata (e){
      if(e.key =="Enter"){
        fetch(`${this.api_url}weather?q=${this.inputvalue}&units=metric&APPID=${this.weather_key}`)
        .then(res => res.json())
        .then(this.setData)
      }
    },
    setData(data){
      console.log(data,"show info");
      this.weather = data
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.search_bar {
  width: 460px;
  margin: 0 auto;
}
</style>
