<template>
<section class="blobs">
     <div class="blob">
          <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
               <path d="M42.4,-44.9C57.9,-37.5,75.6,-27,83.1,-10.7C90.6,5.5,88.1,27.4,74.6,35.7C61.1,44,36.6,38.7,17.4,44.2C-1.9,49.7,-15.9,66.1,-30.5,67.7C-45.1,69.4,-60.1,56.4,-71.4,39.8C-82.6,23.2,-90,3,-82,-9.5C-73.9,-22.1,-50.3,-27,-34.1,-34.3C-17.8,-41.6,-8.9,-51.4,2.3,-54.1C13.4,-56.8,26.9,-52.4,42.4,-44.9Z" transform="translate(100 100)" />
          </svg>
     </div>
     <div class="blob">
          <svg viewBox="0 0 100 100" >
               <path d="M76,63Q71,76,57,79Q43,82,29.5,74.5Q16,67,16,50.5Q16,34,29,24Q42,14,60,14Q78,14,79.5,32Q81,50,76,63Z"/>
          </svg>
     </div>
</section>
<section class="search">
     <div>
          <input type="text" placeholder="Search..." v-model="searchText" @keypress="fetchWeather">
     </div>
</section>
<section class="box" v-if="show">
     <span></span>
     <span></span>
     <span></span>
     <span></span>
     <h1>{{ data.sys.country }}, {{ data.name }}</h1>
     <p class="one">{{ Math.floor(data.main.temp) }} K</p>
     <p class="two">{{ data.weather[0].main }}</p>
</section>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
     name: "indexPage",
     data(){
          return{
               searchText: "",
               show: false,
               api: "https://api.openweathermap.org/data/2.5/weather?",
               api_key: "802f825e97e23c19e2d1548a387ff4a5",
               data: ""
          }
     },
     methods:{
          fetchWeather(e){
               if(e.key == "Enter"){
                    this.show = true;
                    fetch(`${this.api}q=${this.searchText}&appid=${this.api_key}`)
                    .then(res => {
                         return res.json()
                    }).then(response => {
                         this.data = response;
                         console.log(this.data);
                    });
               }
          }
     }
})
</script>


<style scoped>

</style>
