<template>
  <div class="profileView p-4">
    <!-- ICONOS -->
    <!-- <div class="icons flex justify-between h-5 mb-8">
      <img src="/icons/arrow-left.svg" alt="">
      <img src="/icons/list.svg" alt="">
    </div> -->

    <p class="title text-xl font-bold mb-8">My Profile</p>

    <!-- MAIN -->
    <div class="main flex flex-col items-center mb-8">

      <div class="main_img">
        <div class="user_img h-20 aspect-square bg-gray-300 bg-center bg-cover rounded-full"></div>
      </div>

      <p class="text-xl font-bold my-4">{{ userData.username }}</p>

      <p class="text-gray-400 text-center">{{ userData.profileText }}</p>

      <p class="text-gray-400 text-center">Lorem ipsum dolor.</p>

    </div>

    <!-- STATS -->
    <div class="cards flex justify-between">
      <div class="card text-center">
        <p class="text-gray-400">Photos</p>
        <p class="font-bold">{{ userData.photos }}</p>
      </div>
      <div class="card text-center">
        <p class="text-gray-400">Followers</p>
        <p class="font-bold">{{ userData.followers }}</p>
      </div>
      <div class="card text-center">
        <p class="text-gray-400">Posts</p>
        <p class="font-bold">{{ userData.posts }}</p>
      </div>
    </div>
    


    <!-- GRID -->
    <div class="p-8">
      <div class="grid grid-cols-2 gap-8">
        <div
          class="rounded-xl col-span-1 row-span-2 h-full w-full aspect-square bg-gray-300  bg-cover bg-center">
        </div>
        <div class="rounded-xl aspect-square bg-gray-300 bg-cover bg-center"></div>
        <div class=" rounded-xl aspect-square bg-gray-300  bg-cover bg-center"></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import axios from 'axios';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'profileView',
  data() {
    return {
      userData: [] as any[any]
    }
  },
  async mounted() {
    //obtengo usuario actual
    const username = this.$route.params.username

    //obtengo todos los usuarios del json
    const usersData = await axios.get('http://localhost:8081/userdata.json')
    
    //busco usuario actual
    usersData.data.forEach( (user:any) => {
      if(user.username == username){
        this.userData = user
      }
    });
  },
})
</script>

