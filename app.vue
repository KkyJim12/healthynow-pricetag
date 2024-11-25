<template>
  <main class="h-screen bg-gray-300 p-20">
    <div class="flex flex-col space-y-10">
      <div class="bg-white shadow-md w-2/6 rounded-xl p-5">
        <div class="flex flex-col space-y-3">
          <h4 class="text-2xl font-semibold">Product Information</h4>
          <hr />
          <input v-model="title" class="px-4 py-2 rounded shadow-md focus:outline-none border border-gray-200"
            type="text" placeholder="Title" />

          <input v-model="price" class="px-4 py-2 rounded shadow-md focus:outline-none border border-gray-200"
            type="number" placeholder="Price" />

        </div>
      </div>
      <div class="bg-white h-40 w-72 p-2">
        <div class="flex flex-col space-y-2 border-2 border-orange-400 h-full p-3 relative">
          <h1 class="font-semibold line-clamp-2">{{ title }}</h1>
          <h4 class="text-4xl font-bold absolute right-3 bottom-3 flex items-center">
            <span>{{ price }}</span>
            <span class="text-2xl font-semibold">฿</span>
          </h4>
        </div>
      </div>
    </div>
  </main>
</template>


<script setup>
import { ref } from 'vue'

const title = ref('Lorem, ipsum dolor sit amet consectetur adipisicing elit. Vero quod consequuntur ad, obcaecati repellendus accusantium totam harum vel molestiae voluptate, sed maiores quae suscipit corrupti ratione nihil officiis reprehenderit odit.')
const price = ref(888)
const description = ref('Lorem, ipsum dolor sit amet consectetur adipisicing elit. Vero quod consequuntur ad, obcaecati repellendus accusantium totam harum vel molestiae voluptate, sed maiores quae suscipit corrupti ratione nihil officiis reprehenderit odit.')
</script>