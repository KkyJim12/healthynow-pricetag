<template>
  <main
    :class="
      stage === 1
        ? 'min-h-screen p-20 bg-gray-300'
        : 'min-h-screen px-20 py-12 bg-gray-300'
    "
  >
    <div v-if="stage === 1" class="flex flex-col space-y-10">
      <div class="w-2/6 p-5 bg-white shadow-md rounded-xl">
        <div class="flex flex-col space-y-3">
          <h4 class="text-2xl font-semibold">Product Information</h4>
          <hr />
          <input
            v-model="code"
            class="px-4 py-2 border border-gray-200 rounded shadow-md focus:outline-none"
            type="text"
            placeholder="Code"
          />

          <input
            v-model="title"
            class="px-4 py-2 border border-gray-200 rounded shadow-md focus:outline-none"
            type="text"
            placeholder="Title"
          />

          <input
            v-model="price"
            class="px-4 py-2 border border-gray-200 rounded shadow-md focus:outline-none"
            type="text"
            placeholder="Price"
            pattern="\d*"
            maxlength="4"
          />
        </div>
        <button
          @click="save"
          class="w-full py-2 mt-2 text-white duration-200 bg-green-500 rounded shadow-md hover:bg-green-600"
          type="button"
        >
          Save
        </button>
        <button
          @click="confirm"
          class="w-full py-2 mt-2 text-white duration-200 bg-blue-500 rounded shadow-md hover:bg-blue-600"
          type="button"
        >
          Export
        </button>
      </div>
      <div class="grid grid-cols-12 gap-5">
        <div
          v-for="(priceTag, index) in priceTags"
          :key="index"
          class="col-span-2"
        >
          <div class="flex flex-col space-y-3">
            <div class="w-full h-40 p-2 bg-white">
              <div
                class="relative flex flex-col h-full p-3 space-y-2 border-2 border-orange-400"
              >
                <p
                  class="absolute flex items-center text-xs font-bold text-gray-800 top-1 right-2"
                >
                  [{{ priceTag.code }}]
                </p>
                <h1 class="font-semibold text-gray-800 line-clamp-2">
                  {{ priceTag.title }}
                </h1>
                <div class="z-40">
                  <img
                    class="absolute w-24 bottom-3"
                    src="/img/logo.png"
                    alt="logo"
                  />
                </div>
                <h4
                  class="absolute flex items-center text-5xl font-bold text-gray-800 right-3 bottom-3"
                >
                  <span>{{ priceTag.price }}</span>
                  <span class="overflow-hidden text-3xl font-semibold">฿</span>
                </h4>
              </div>
            </div>
            <button
              @click="remove(index)"
              type="button"
              class="w-full py-2 text-white duration-200 bg-red-500 rounded hover:bg-red-600"
            >
              Remove
            </button>
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <div class="grid grid-cols-12 gap-5">
        <div
          v-for="(priceTag, index) in priceTags"
          :key="index"
          class="col-span-6"
        >
          <div class="flex flex-col space-y-3">
            <div class="w-full h-40 p-2 bg-white border">
              <div
                class="relative flex flex-col h-full p-3 space-y-2 border-2 border-orange-400"
              >
                <p
                  class="absolute flex items-center text-xs font-bold text-gray-800 top-1 right-2"
                >
                  [{{ priceTag.code }}]
                </p>
                <h1 class="font-semibold text-gray-800 line-clamp-2">
                  {{ priceTag.title }}
                </h1>
                <div class="z-40">
                  <img
                    class="absolute w-24 bottom-3"
                    src="/img/logo.png"
                    alt="logo"
                  />
                </div>
                <h4
                  class="absolute flex items-center text-5xl font-bold text-gray-800 right-3 bottom-3"
                >
                  <span>{{ priceTag.price }}</span>
                  <span class="overflow-hidden text-3xl font-semibold">฿</span>
                </h4>
              </div>
            </div>
          </div>
        </div>
      </div>
      <button
        @click="back"
        class="absolute w-20 h-20 text-xl text-white duration-200 bg-blue-500 rounded-full opacity-0 bottom-10 right-10 hover:opacity-100"
      >
        Back
      </button>
    </div>
  </main>
</template>

<script setup>
import { ref, reactive } from "vue";

const stage = ref(1);

const code = ref("P-000");

const title = ref(
  "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Vero quod consequuntur ad, obcaecati repellendus accusantium totam harum vel molestiae voluptate, sed maiores quae suscipit corrupti ratione nihil officiis reprehenderit odit."
);
const price = ref(888);

const priceTags = ref([]);

const save = () => {
  priceTags.value.push({ code: code, title: title.value, price: price.value });
};

const remove = (index) => {
  priceTags.value.splice(index, 1);
};

const confirm = () => {
  stage.value = 2;
};

const back = () => {
  stage.value = 1;
};
</script>
