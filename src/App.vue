<template>
  <div id="app">
    <div class="search-box">
      <input
        type="text"
        class="searchbar"
        placeholder="Search..."
        v-model="query"
        @keypress="fetchWeather"

      />
      <div class="location-box" v-if="isVisible">
        <div class="location">{{weather.name}},{{weather.country}}</div>
        <div class="date">{{weather.localtime}}</div>
      </div>
      <div class="normal" v-else>Search a place to see the current weather</div>

      <div class="weather" v-if="isVisible" >
        <div class="temp">{{Math.round(info.temp_c)}}&deg; C</div>
        <div class="status">{{info.condition.text}}
        </div>
       <div class="iconholder">
          <img :src="link" alt="icon">
       </div>
      </div>
  </div>
  <footer>
    Copyright &copy; my weatherapp Suma373 All Rights reserved 2022
  </footer>
</div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      api_key: "",
      base_url: "https://weatherapi-com.p.rapidapi.com/current.json",
      query: '',
      weather: {},
      info:{},
      link:''
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key === "Enter" || e.keyCode === 13) {
        fetch(`${this.base_url}?q=${this.query}`,{
          method: 'GET',
          headers:{'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com','X-RapidAPI-Key': 'bd'
          }
        })
          .then((response) => {
            return response.json();
          })
          .then(this.setResults);
      }
    },
    
    },
  },
};

</script>

<style>
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  overflow-x: hidden;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
body {
  height: 100vh;
  width: 100vw;
}
#app{
  height: 100%;
  width: 100%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center; 
  background: url("./assets/cold-bg.jpg") no-repeat center center/cover;
  animation:weather 15s ease-in-out infinite;
  transition: animation 600ms;
}
@keyframes weather{
  33%{
    background:url('./assets/warm-bg.jpg') no-repeat center/cover;
  }
  66%{
    background:url('./assets/rainy-bg.jpg') no-repeat center/cover;
  }
}

.normal{
  font-size:1.5rem;
  padding:10px;
  text-align: center;
  margin-top:5rem;
}
.search-box {
  height: 25rem;
  width: 25rem;
  color: white;
  border-radius: 20px;
  background: rgba(19, 19, 51, 0.568);
  box-shadow: 0 0 3px black;
}
.searchbar {
  height: 3rem;
  font-size: 1.2rem;
  margin-top: 1rem;
  width: 100%;
  background: transparent;
  color: white;
  padding: 10px;
  border: none;
  border-bottom: 2px solid black;
  outline: none;
}
input::placeholder {
  color: white;
}

/* location info container */
.location-box {
  height: 6rem;
  padding: 10px;
  text-align: center;
  color: white;
  width: 100%;
  background: rgba(0, 0, 0, 0.301);
}
.location {
  font-size: 1.5rem;
   color:yellow;
  font-weight: 400;
  text-shadow: 0 0 2px black;
}

.date {
  font-size: 1.2rem;
}
.weather {
  height: 8rem;
  width: 12rem;
  margin: 1rem auto;
  background: rgba(0, 0, 0, 0.301);
  box-shadow: 0 0 3px white;
  border-radius: 10px;
  text-align: center;
}
.temp {
  font-size: 3.5rem;
  font-weight:800;
  font-style: italic;
}
.status {
  height:3rem;
  width:100%;
  color:yellow;
  font-size: 1.2rem;
}
.iconholder{
  margin-top:10px;
  text-align: center;
}
footer{
  width:100%;
  height:2rem;
  background: rgba(0, 0, 0, 0.322);
  position: fixed;
  bottom:0;
  font-size:1.1rem;
  color:yellow;
  text-align: center;
}

@media screen and (max-width:460px){
  #app{
    height:100vh;
    width:100vw;
  }
 .search-box{
   width:20rem;
 }
 .weather{
   width:10rem;
 }
 .temp{
   font-size:2.8rem;
 }
 .status{
   font-size:1rem;
 }
 .iconholder{
   margin-top:15px;
 }
 footer{
   font-size:1rem;
 }
}
</style>
