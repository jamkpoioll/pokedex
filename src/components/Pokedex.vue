<template>
  <div>
    <input class="Moji" v-model="value" />
    <button @click="handleClick">検索</button>
  </div>
  
  <img class="Image" v-if="data!==null" :src="data.sprites.front_shiny" />
  <p class="Name" v-if="data">{{ data.name }}</p>
</template>

<script lang="ts">
import {defineComponent} from "vue"

interface Data {
  value: string;
  data: any;
}

export default defineComponent({
  data(): Data{
    return{
      value: "",
      data: null
    }
  },
  methods: {
    async handleClick(){
      const res = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.value}`)
      const json = await res.json()
      this.data = json
    }
  }
})
</script>

<style>
.Image {
  width: 300px;
  height: 300px;
}
.Name {
  font-size: 30px;
}
.Moji {
  width: 300px;
  height: 30px;
  margin-right: 10px;
}
</style>