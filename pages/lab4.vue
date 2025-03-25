<template>
    <main class="flex flex-row gap-4 justify-center items-center h-screen bg-gradient-to-b from-gray-200 to-blue-300 hover:to-red-300 flex-wrap">
      <div>
        <label>
          <input class="mx-2" type="radio" value="bill" v-model="selectedpic">Bill
        </label>
        <label>
          <input class="mx-2" type="radio" value="bill" v-model="selectedpic">Bill
        </label>
        <label>
          <input class="mx-2" type="radio" value="bill" v-model="selectedpic">Bill
        </label>
      </div>
      <div class="flex flex-row gap-2 border-blue-500 border-1 bg-blue-300 w-72 h-auto items-center hover:border-red-500 border-2 hover:bg-red-300 rounded-xl">
        <img :src="pic1.image" class="w-60 h-68 pt-2">
        <p class="text-black text-xl">{{pic1.name}}</p>
      </div>
      <div class="flex flex-row gap-2 border-blue-500 border-1 bg-blue-300 w-72 h-auto items-center hover:border-red-500 border-2 hover:bg-red-300 rounded-xl">
        <img :src="pic2.image" class="w-60 h-68 pt-2">
        <p class="text-black text-xl">{{pic2.name}}</p>
      </div>
      <div class="flex flex-row gap-2 border-blue-500 border-1 bg-blue-300 w-72 h-auto items-center hover:border-red-500 border-2 hover:bg-red-300 rounded-xl">
        <img :src="pic3.image" class="w-60 h-68 pt-2">
        <p class="text-black text-xl">{{pic3.name}}</p>
      </div>
    </main>
  </template>
  
  <script setup lang="ts">
  import{reactive} from 'vue'
  interface stking{
    name:string,
    image:string
  }
  const pic1 =reactive<stking>({
    name:'bill',
    image:"/img/ben.png"
  })
  const pic2 =reactive<stking>({
    name:'beverly',
    image:"/img/beverly.png"
  })
  const pic3 =reactive<stking>({
    name:'Dracula',
    image:"/img/Dracula.png"
  })
  
  const gepnic= reactive<stking[]>([
    {name:'eddie', image:"/img/eddie.png"},
    {name:'henry', image:"/img/henry.png"},
    {name:'mike', image:"/img/mike.png"}
  ])
  
  const selectedpic = ref<string>('')
  </script>
  
  <style scoped>
    .blockcap{
      @apply flex flex-col gap-2 border-blue-500 border bg-blue-300 w-72 h-auto items-center hover:border-red-500 gover:border-4 hover:bg-red-300 rounded-xl;
    }
    .blockfor{
      @apply flex flex-col gap-2 border-blue-500 border bg-blue-300 w-72 h-auto items-center hover:border-yellow-500 gover:border-4 hover:bg-yellow-300 rounded-xl;
    }
  </style>
  