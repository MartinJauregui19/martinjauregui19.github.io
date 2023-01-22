<template>
    <div class="footer_img flex gap-8 items-center rounded-b-xl">
        <div class="user_img h-20 aspect-square bg-gray-400 bg-center bg-cover rounded-full"></div>
            <div class="footer_txt ">
                <p class="font-bold">{{ name }}</p>
                <p class="text-gray-400">{{ text }}</p>
            </div>
    </div> 
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'userItem',
    props:{
        image: String,
        name: String,
        text: String
    }
})
</script>