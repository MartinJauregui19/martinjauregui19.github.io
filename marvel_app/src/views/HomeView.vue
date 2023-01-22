<template>
  <!--Swiper-->
  <section class="swiper">
    <div class="aspect-video bg-gray-300 bg-cover bg-center relative"
         style="background-image: url('/img/spider-cover.jpg');">
      <div class="gradient w-3/4 h-full bg-gradient-to-r from-black to-transparent absolute top-0 left-0">
      </div>
      <div class="comicInfo w-full flex flex-col gap-2 text-white p-4 absolute bottom-0 left-0">
          <p class="font-bold">INTO THE SPIDER-VERSE</p>
          <p class="text-sm">SPIDER-VERSE 10 lorem</p>
          <div class="score flex gap-2">
            <div class="scoreIcon h-6 w-3 bg-gradient-to-b from-orange-300 to-orange-600" style="mask-image: url('/img/icons/lightning.svg');mask-position:center;mask-size:cover;mask-repeat: no-repeat;"></div>
            <p>10</p>
          </div>
      </div>     
    </div>
  </section>

  <div class="content py-4 flex flex-col gap-8">
    <!--Cards Section-->
    <section class="card">
      <!--Title-->
      <div class="sectionTitle flex justify-between items-center px-4 mb-4">
        <p class="text-xl font-bold uppercase">YOUR FAVOURITE HEROES</p>
        <div class="button bg-red-600 py-1 px-4 rounded-md">
          <div class="icon1 h-6 w-6 bg-white" style="mask-image:url('/img/icons/arrow-right.svg'); mask-position:center; mask-size:cover; mask-repeat:no-repeat;"></div>
        </div>
      </div>

      <!--Cards-->
      <div class="cards px-4 overflow-x-auto flex gap-4">
        <div  class="card flex-none w-1/5 "
              v-for="character,index in characters"
              :key="index">
          <div  class="cardImage w-full aspect-square bg-gray-300 rounded-full bg-cover bg-center mb-1"
                :style="'background-image: url('+character.thumbnail.path+'.'+character.thumbnail.extension+')'">
          </div>
          <p class="text-sm text-gray-600 text-center truncate">{{  character.name }}</p>
        </div>
      </div>
    </section>

    <!--Comics-->
    <section class="comics">
    <div class="sectionTitle flex justify-between items-center px-4 mb-4">
      <p class="text-xl font-bold uppercase">TOP RATED COMICS</p>
      <div class="button bg-red-600 py-1 px-4 rounded-md">
        <div class="icon1 h-6 w-6 bg-white" style="mask-image: url('/img/icons/arrow-right.svg');mask-position:center;mask-size:cover;mask-repeat: no-repeat;"></div>
      </div>
    </div>
    <div class="comics px-4 overflow-x-auto flex gap-4">
      
        <div class="comicCard w-5/12 flex-none" v-for="comic,index in comics" :key="index">
          <router-link :to="'/comic/'+comic.id">
            <div  class="comicCover w-full aspect-[2/3] bg-red-300 mb-2 bg-cover bg-center"
                  :style="'background-image: url('+comic.thumbnail.path+'.'+comic.thumbnail.extension+')'">
            </div>
            <div class="comicInfo flex flex-col gap-2">
              <p class="font-bold">{{ comic.title   }}</p>
              <p class="text-sm text-gray-600">{{ comic.series.name }}</p>
              <div class="score flex gap-2">
                <div class="scoreIcon h-6 w-3 bg-gradient-to-b from-orange-300 to-orange-600" style="mask-image: url('/img/icons/lightning.svg');mask-position:center;mask-size:cover;mask-repeat: no-repeat;"></div>
                <p>5.6</p>
              </div>
            </div>
          </router-link>
        </div>
      
    </div>
    </section>
  </div>
</template>

<script lang="ts">
//import axios
import axios from 'axios'
import {UUID} from 'uuid-generator-ts'
import {Md5} from 'ts-md5'

//create vue instance
import { defineComponent } from 'vue'

export default defineComponent({
  name: "HomeView",
  data() {
      return{
        characters: [] as any[any],
        comics: [] as any[any]
      }
  },
  async mounted(){
    //1RA LLAMADA A LA API
    //generar uuid
    let uuid = new UUID() as any[any]

    //get random string
    let ts = uuid.str

    //set keys
    const publicKey = '3d74b9bbea76f4930ee53ba06630a231'
    const privateKey = 'ae8ff3777f36e88adbf59036e4d748a555a83d2f'

    //create hash
    let hash = Md5.hashStr(ts+privateKey+publicKey)

    //get characters from api
    let response = await axios.get('https://gateway.marvel.com:443/v1/public/characters?nameStartsWith=spider&limit=6&apikey='+publicKey+'&hash='+hash+'&ts='+ts)

    this.characters = response.data.data.results

    console.log(this.characters)

    //2DA LLAMADA A LA API

    //generar uuid
    uuid = new UUID() as any[any]

    //get random string
    ts = uuid.str

    //create hash
    hash = Md5.hashStr(ts+privateKey+publicKey)

    //get comic/characters from api
    response = await axios.get('https://gateway.marvel.com:443/v1/public/comics?titleStartsWith=spider&limit=6&apikey='+publicKey+'&hash='+hash+'&ts='+ts)

    this.comics = response.data.data.results

    console.log(this.comics)
  }
})
</script>


<!--//pantlla 1
quiero los comica que empiecen con 'spider'

comics= data{
          results: [
            0: {
              titulo: este es el comic 1,
              id: 1
            },
            1: {
              titulo: comic de spider 2,
              id: 2
            }
          ]
        }

//armo v-for
<div v-for="item,index in comic" :key="index">
 <router-link :to="'/comic/'+item.id">
    <p>{{ item.titulo }}</p>
  </router-link>
</div>


//pantalla 2
quiero el comic 1

data{
  results: [
    0: este el comic 3
  ]
} -->
