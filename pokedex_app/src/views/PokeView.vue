<template>
  <!-- <div class="about">
    <p>{{  requestedPokemon.name }}</p>
  </div> -->
  <div class="flex flex-col gap-4">
      <!-- NAVBAR -->
      <nav class="flex items-center justify-between pt-8 px-8 pb-4 text-white">
        
        <!-- <p class="bg-blue-500" v-for="pokemon,index in pokemons" :key="index">{{ pokemon.name }}</p> -->
        <div class="flex gap-4 items-center"> 
              <div class="buttons flex justify-between">
                <router-link  to="/">
                  <div class="bg-white w-5 h-5" style="-webkit-mask-image: url('/img/icons/arrow-left.svg'); mask-image: url('/img/icons/arrow-left.svg');"></div>
                </router-link>
              </div>
          <p class="text-xl">Pokedex</p>
        </div>
        <div class="classN">
          <p class="number">{{ '#'+requestedPokemon.id }}</p>
        </div> 
      </nav>
      <div class="top rounded-3xl overflow-hidden relative mx-8" :class="(requestedPokemon.types) ? colors[requestedPokemon.types[0].type.name] : ''">

      <div class="bubble w-2/5 aspect-square bg-gradient-to-b from-white to-transparent opacity-25 -rotate-45 rounded-full absolute -top-8 -left-8"></div>
      
      <div class="pokeMask w-full aspect-square bg-white bg-opacity-40 absolute -bottom-28 -right-28" style="mask-image:url(/img/pokeball.svg);mask-position:center; mask-size:cover"></div>

      <div class="pokePic w-1/2 flex mx-auto aspect-square relative z-10">
        <img v-if="requestedPokemon.sprites" :src="requestedPokemon.sprites.front_default" alt="">
      </div>
    </div>

    <!-- MAIN -->
    <div class="infoCard p-4 text-white">
      <div class="name text-center mb-2">
        <p class="pokeName text-xl font-bold uppercase">{{   requestedPokemon.name }}</p>
      </div>

      <div class="flex gap-4 justify-center mb-4">
        <div  class="chip text-center text-xs w-1/3  py-1 px-2 rounded-full"
              :class="colors[types.type.name]"
              v-for="types,typeIndex in requestedPokemon.types" :key="typeIndex">
          <p class="-mt-1 text">{{ types.type.name }}</p>
        </div>
      </div>  

      <div class="h&w flex justify-center gap-4">
        <div class="hight text-center w-1/3">
          <p> {{ (requestedPokemon.height * 10) + " cm"}}</p>
          <p class=" text-gray-500">Height</p>
        </div>

        <div class="weight text-center  w-1/3">
          <p> {{ requestedPokemon.weight + " Kg"}}</p>
          <p class=" text-gray-500">Weight</p>
        </div>
      </div>
    </div>

     <!-- BASE STATS -->

     <div class="stats flex flex-col gap-4 text-white px-8 mb-8">
        <p class="text-center">Base Stats</p>
        <div class="stat flex gap-4" v-for="stats,index in requestedPokemon.stats" :key="index">
          <p class="statName w-1/3 text-xs">{{ statsLabels[stats.stat.name] }}</p>
          <div class="statBar w-2/3 rounded-xl bg-white overflow-hidden relative flex items-center justify-center">
            <div class="h-full text-right px-2 rounded-xl absolute top-0 left-0 w-0 trasition-all" :class="statsColors[stats.stat.name]" :style="'width: calc('+stats.base_stat+' * 100% / 300)'">
            </div>
            <p class="text-xs text-black">{{ stats.base_stat + '/300'}}</p>
          </div>
        </div>
      </div>
  </div>
</template>

<script lang="ts">
import axios from 'axios'
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'pokeView',
  data() {
    return {
      requestedPokemon: [] as any[any],
      statsColors:{
        hp:"bg-red-500",
        attack:"bg-yellow-600",
        defense:"bg-blue-500",
        'special-attack':"bg-orange-600",
        'special-defense':"bg-sky-300",
        speed:"bg-green-600"
      } as any[any],
      statsLabels:{
        attack: 'ATK',
        hp:"HP",
        defense:"DEF",
        'special-attack':"SA",
        'special-defense':"SD",
        speed:"SPD"
      } as any[any],
      colors:{
            grass: 'bg-green-400',
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
            dragon:'bg-red-500',
            flying:'bg-sky-300'
          } as any[any]

    }
  },
  async mounted() {
    //recupero el id de la url (de la variable que definí en el router)
    const id = this.$route.params.pokemonid

    //hago la llamada a la api para buscar el pokemon con ese id
    const response = await axios.get('https://pokeapi.co/api/v2/pokemon/' + id)

    //ASIGNO LA RESPUESTA A LA VARIABLE DINAMICA PARA USAR EN MAQUETA
    this.requestedPokemon = response.data

    console.log(response.data)

  },
})
</script>