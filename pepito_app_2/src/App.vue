<template>
  <!-- <p v-if="forecast.current_weather">{{ forecast.current_weather.temperature }}</p> -->
<div class="p-8 bg-cover bg-center" style="background-image: url('/img/imagen1.jpg')"> 
  <div class="head mb-4">
    <div class="flex flex-col justify-center items-center gap-4 mb-4">
      <p class="text-4xl">Ciudad</p>
      <p class="text-7xl" v-if="forecast.current_weather">{{ forecast.current_weather.temperature }}°C</p>
      <p class="font-semibold">{{ currentStatus }}</p>
    </div>
    <div class="temperature flex justify-center gap-4">
      <p class="font-semibold">Temp Max: {{ tempMax }}</p>
      <p class="font-semibold">Temp Min: {{ tempMin }}</p>
    </div>
  </div>

  <div class=" bg-sky-300 bg-opacity-50 rounded-md py-4 flex flex-col gap-4">
    <div class= "text-white text-xl flex justify-center items-center gap-12" v-for="hourlyData,index in hourly" :key="index">
      <p>{{  hourlyData.time }}</p>
      <img src="" alt="icono">
      <p>{{ hourlyData.temperature+'°C' }}</p>
    </div>
  </div>
</div>     
</template>

<script lang="ts">
import axios from 'axios'

import { defineComponent } from 'vue'

export default defineComponent({
  name: 'App',
  data(){
    return {
      forecast: [] as any[any],
      tempMin: 0,
      tempMax: 0,
      currentStatus: '',
      weatherCodes:{
        0: 'Despejado',
        1: 'Mayormente despejado'
      } as any[number],
      hourly: [] as any[any]
    }
  },
  async mounted() {
      //llamar a la api y guardar su respuesta en la varable response
      const response = await axios.get('http://api.open-meteo.com/v1/forecast?current_weather=true&latitude=-31.40&longitude=-58.02&timezone=America/Argentina/Buenos_Aires&daily=temperature_2m_max,temperature_2m_min&hourly=temperature_2m')
      
      //imprimimos el resultado del data (información)
      console.log(response.data)

      //guardamos el data (información) en la variable forecast (variable dinámica)
      this.forecast = response.data

      //obtengo estado
      const weathercode = this.forecast.current_weather.weathercode 
      this.currentStatus = this.weatherCodes[weathercode]

      //obtengo min y max
      this.getTodayMinMax()

      //obtengo temperaturas por hora
      this.getHourlyTemps(this.forecast.hourly)
  },
  methods:{
    getTodayMinMax(){
      const today= new Date()

      const dayNbr= today.getDay()

      this.tempMax= this.forecast.daily.temperature_2m_max[dayNbr]
      this.tempMin= this.forecast.daily.temperature_2m_min[dayNbr]
    },
    getHourlyTemps(hourly:any){
      for(let i = 0; i <= 23; i++){
        this.hourly.push({
          time: hourly.time[i].slice(11),
          temperature: hourly.temperature_2m[i]
        })
      }

      console.log(this.hourly)
    }
  }
  
});
</script>

