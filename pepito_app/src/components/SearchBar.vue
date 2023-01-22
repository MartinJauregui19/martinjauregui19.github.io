<template>
    <div class="mb-8 px-8 py-4 bg-gray-100 rounded-full">
        <div class="flex gap-4">
            <div class="searchButton">
                <svg width="30" height="30" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path d="m21.75 20.692-5.664-5.664a8.264 8.264 0 1 0-1.06 1.061l5.664 5.664 1.06-1.06ZM3 9.753a6.75 6.75 0 1 1 6.75 6.75A6.758 6.758 0 0 1 3 9.753Z"></path>
                </svg>
            </div>
            <input class="bg-transparent outline-none" type="text" placeholder="search">
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'searchBar'
})
</script>