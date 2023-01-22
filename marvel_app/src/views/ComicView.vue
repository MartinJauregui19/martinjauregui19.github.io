<template>
  <div class="comic-cover p-8 flex flex-col gap-8">
    <div class="navbar">
      <div class="icon h-5 w-6">
        <svg fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
          <path d="m10.5 19.5 1.057-1.058-5.685-5.692H21v-1.5H5.872l5.685-5.692L10.5 4.5 3 12l7.5 7.5Z"></path>
        </svg>
      </div>
    </div>
    
    <section class="comic flex gap-4">
      <div class="cover w-1/2">
        <div  class="aspect-[2/3] w-full bg-red-300 bg-center bg-cover"
              :style="'background-image: url('+comic.thumbnail.path+'.'+comic.thumbnail.extension+')'"
              v-if="comic.thumbnail"></div>
      </div>
      
      <div class="comicInfo flex flex-col gap-2 w-1/2">
        <p class="font-bold">{{ comic.title }}</p>
        <p class="text-sm text-gray-600">text</p>
        <div class="score flex gap-2">
          <div class="scoreIcon h-6 w-3 bg-gradient-to-b from-orange-300 to-orange-600"
            style="mask-image: url('/img/icons/lightning.svg');mask-position:center;mask-size:cover;mask-repeat: no-repeat;">
          </div>
          <p>5.6</p>
        </div>

        <div class="flex flex-col">
          <p class="text-sm font-bold">Also read</p>
          <div class="otherComics flex justify-between items-center py-1 border-b border-black"
                v-for="i in 3" :key="i">
            <p class="text-sm truncate">Lorem, ipsum dolor elit.</p>
            <p>Icon</p>
          </div>
        </div>
      </div>
    </section>

    <div class="flex flex-col gap-2">
      <p>FEATURED CHARACTERS</p>
      <p>Captain America</p>
    </div>

    <div class="sypnosis">
      <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Error molestias facilis maiores hic veniam labore,
        cum in accusamus eos asperiores! Iste vero nemo fugit officiis voluptatem culpa alias reiciendis soluta.</p>
    </div>

    <div class="button w-full bg-red-600">button</div>
  </div>

</template>


<script lang="ts">
//import axios
import axios from 'axios'
import { UUID } from 'uuid-generator-ts'
import { Md5 } from 'ts-md5'

//create vue instance
import { defineComponent } from 'vue'

export default defineComponent({
  name: "HomeView",
  data() {
    return {
      comic: [] as any[any]
    }
  },
  async mounted() {
    //recupero el id del comic actual
    const id = this.$route.params.idComic

    console.log(id)


    //1RA LLAMADA A LA API
    //generar uuid
    let uuid = new UUID() as any[any]

    //get random string
    let ts = uuid.str

    //set keys
    const publicKey = '3d74b9bbea76f4930ee53ba06630a231'
    const privateKey = 'ae8ff3777f36e88adbf59036e4d748a555a83d2f'

    //create hash
    let hash = Md5.hashStr(ts + privateKey + publicKey)

    //get characters from api
    let response = await axios.get('https://gateway.marvel.com:443/v1/public/comics/'+id+'?apikey='+publicKey+'&hash='+hash+'&ts='+ts)

    this.comic = response.data.data.results[0]

    console.log(this.comic)
  }
})
</script>