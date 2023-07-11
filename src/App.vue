<script setup>
import { computed } from 'vue';
import submission from './seed'
let seed = submission

const sorted = computed(()=>{
  return [...seed].sort((a,b)=>b.votes - a.votes);
})

const upvote = (seedId) => {
  seed.find((el) => {
    if (seedId === el.id) { 
      el.votes++
      seed = [el, ...seed]
    }

    console.log(seed)
  })
}


</script>

<template>
  <div class="flex flex-col items-center justify-center gap-4">
    <h1 class="text-center text-3xl font-bold pt-4">Up Vote</h1>
   
    <div class="w-1/2 shadow-lg border py-3 flex gap-10" :key="seeds.id" v-for="seeds in sorted" :class="{'border-blue-500' : seeds.votes>=20}">
      <div>
        <img src="./assets/profile.png" alt="" />
      </div>
      <div class="flex flex-col gap-4 pt-5">
        <h2 class="text-blue-500 text-2l font-semibold">
         {{ seeds.title }}
          <span class="bg-slate-100 text-black p-[2px] rounded">#4</span>
        </h2>

        <p class="text-xl">{{ seeds.description }}</p>
        <div class="flex gap-2">
          <p>Submitted by:</p>
          <img :src="seeds.avatar" alt="" class="h-5" />
        </div>
      </div>
   
      <div class="flex gap-2">
        <p @click="upvote(seeds.id)">2</p>
        <p class="text-blue-500">{{ seeds.votes }}</p>
      </div>
    </div>
    
  </div>
</template>

<style scoped></style>
