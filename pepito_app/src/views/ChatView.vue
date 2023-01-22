<template>
    
    <div class="p-8">
        <!-- ICONOS -->
        <!-- <div class="icons flex justify-between h-5 mb-8">
            <img src="/icons/arrow-left.svg" alt="">
            <img src="/icons/list.svg" alt="">
        </div> -->

        <p class="text-xl font-bold mb-8">Conversation</p>

        <!-- SEARCH-BAR -->
        <SearchBar></SearchBar>

        <!-- CONTACTS -->
    
        <div class="contact flex flex-col gap-4">
            <UserItem v-for="message,index in messages" :key="index" :name="message.name" :text="message.text"></UserItem> 
            <img class="h-16 bg-pink-400 rounded-full fixed bottom-4 right-4 p-4" src="/icons/pen.svg" alt="as">
        </div>
        
    </div>        
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import SearchBar from '@/components/SearchBar.vue';
import UserItem from '@/components/UserItem.vue'

export default defineComponent({
  name: 'chatView',
  components:{
    SearchBar,
    UserItem
  },
  data(vm) {
      return{
        messages:[
          {
            name: 'Adro',
            text: 'Penes'
          },
          {
            name: 'Martín',
            text: 'No gracias'
          },
        ]
      }
  },
  
})

</script>