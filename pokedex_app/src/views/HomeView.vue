<template>
  <div class="p-8 bg-zinc-900">

    <!-- TITLE -->
    <div class="title text-xl font-bold mb-8 text-white">POKEDEX</div>

    <!-- CARDS -->
    <div class="cards grid grid-cols-2 lg:grid-cols-5 gap-4">
      <div class="card p-4 rounded-xl aspect-[4/3] relative cursor-pointer overflow-hidden" :class="colors[pokemon.types[0].type.name]" v-for="pokemon,index in pokemons" :key="index">
        <router-link :to="'/info/'+pokemon.id">
          <div class="info flex flex-col gap-1 text-white">
            <p class="pokeName text-xs font-bold uppercase">{{   pokemon.name }}</p>
            <div class="chip text-xs w-fit bg-white bg-opacity-20 py-1 px-2 rounded-full" v-for="types,typeIndex in pokemon.types" :key="typeIndex">
              <p class="-mt-1">{{ types.type.name }}</p>
            </div>
          </div>
          <div class="pokeMask w-3/4 aspect-square bg-white bg-opacity-40 absolute -bottom-8 -right-8" style="mask-image:url(/img/pokeball.svg);mask-position:center; mask-size:cover"></div>
          <div class="pokePic absolute bottom-0 right-0 w-1/2 aspect-square">
            <img class="w-full" :src="pokemon.sprites.front_default" alt="">
          </div>
        </router-link>
      </div>

      <!-- Skeleton-->
      <div class="card p-4 rounded-xl aspect-[4/3] bg-gray-300 animate-pulse" v-for="i in 10" :key="i" v-show="loading">
      </div>
    </div>
    
    <!--button-->
    <div class="loadMore border border-white bg-white bg-opacity-20 py-2 px-4 text-center text-white rounded-md mt-4" @click="getPokemons()" v-show="pokemons.length > 0 && lastPokemon <= 151">
      <p>Load More</p>
    </div>
  </div>  
</template>

<script lang="ts">
  import axios from 'axios'
  import {defineComponent} from 'vue';

  export default defineComponent ({
      name:'homeView',
      data(){
        return{
          loading: false,
          lastPokemon: 1,
          pokemons:[] as any[any],
          colors:{
            grass: 'bg-green-500',
            fire: 'bg-orange-500',
            water:'bg-sky-400',
            bug:'bg-lime-500',
            electric:'bg-yellow-500',
            normal:'bg-gray-400',
            poison:'bg-violet-400',
            ground:'bg-amber-600',
            fairy:'bg-rose-300',
            fighting:'bg-orange-700',
            psychic:'bg-pink-600',
            rock:'bg-yellow-700',
            ghost:'bg-purple-600',
            ice:'bg-cyan-300',
            dragon:'bg-red-500'
          } as any[any]
        }
      },
      mounted(){
        this.getPokemons()
      },
      methods:{
        async getPokemons(){
          this.loading = true

          const limit = this.lastPokemon + 9 // 20

          while( this.lastPokemon <= limit && this.lastPokemon <= 151){
            let response = await axios.get('https://pokeapi.co/api/v2/pokemon/'+this.lastPokemon)
            this.pokemons.push(response.data)
            this.lastPokemon++
            if(this.lastPokemon == limit){
              this.loading = false
            }
          }
          
        }
        // getColor(type:string){
        //   if(type == 'grass'){
        //     return 'bg-teal-400'
        //   }
        //   else if(type == 'fire'){
        //     return 'bg-red-400'
        //   }
        //   else if(type == 'water'){
        //     return 'bg-sky-300'
        //   }
        //   else if(type == 'bug'){
        //     return 'bg-lime-400'
        //   }
        //   else if(type == 'electric'){
        //     return 'bg-yellow-400'
        //   }
        //   else{
        //     return 'bg-gray-300'
        //   }

        // }
      }
  })
</script>
