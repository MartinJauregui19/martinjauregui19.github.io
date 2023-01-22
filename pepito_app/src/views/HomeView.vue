<template>
    <div class="p-8">
        <div class="user flex justify-between mb-8">
            <div class="flex flex-col">
                <p class="text-gray-400">Hello</p>
                <p class="text-xl font-bold">Gornarova!</p>
            </div>
            <div class="user_img h-20 aspect-square bg-gray-300 bg-center bg-cover rounded-full">
            </div>
        </div> 

        <!-- SEARCH-BAR -->
       <SearchBar></SearchBar>

        <!-- HISTORIAS -->
        <div class="historias flex gap-8 mb-8 p-2 overflow-x-auto">
            <div class="bg-gray-200 h-20 aspect-square rounded-full">
                <p class=""></p>
            </div>

            <div class="user_img h-20 ring ring-pink-400 aspect-square bg-gray-300 bg-center bg-cover rounded-full">
            </div>
            <div class="user_img h-20 ring ring-pink-400 aspect-square  bg-gray-300 bg-center bg-cover rounded-full">
            </div>
            <div class="user_img h-20 ring ring-pink-400 aspect-square  bg-gray-300 bg-center bg-cover rounded-full">
            </div>

        </div>

        <!-- IMAGEN -->
        <div class="img1">
            <div class="aspect-[4/3]  bg-gray-300 bg-cover bg-center rounded-t-xl"></div>

            <div class="footer_img flex justify-between items-center py-4 px-8 bg-gray-100 rounded-b-xl">
                <div class="user_img h-20 aspect-square  bg-gray-300 bg-center bg-cover rounded-full">
                </div>
                <div class="footer_txt">
                    <p class="font-bold">Lola Ponti</p>
                    <p class="text-gray-400">lorem</p>
                </div>

                <div>
                    <img src="/icons/list.svg" alt="">
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import SearchBar from '@/components/SearchBar.vue';

export default defineComponent({
  name: 'profileView',
  components:{
    SearchBar
  }
})
</script>

