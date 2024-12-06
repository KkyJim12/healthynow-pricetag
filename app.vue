<template>
  <main
    :class="
      stage === 1
        ? 'min-h-screen p-20 bg-gray-300'
        : 'min-h-screen px-20 bg-gray-300'
    "
  >
    <div v-if="stage === 1" class="flex flex-col space-y-10">
      <div class="flex gap-x-10">
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
        <div class="w-full p-5 bg-white shadow-md rounded-xl">
          <div class="flex flex-col space-y-3">
            <h4 class="text-2xl font-semibold">Add by JSON</h4>
            <hr />
            <textarea
              v-model="json"
              class="px-4 py-2 border border-gray-200 rounded shadow-md resize-none focus:outline-none"
              placeholder="JSON"
              rows="6"
            ></textarea>
            <button
              @click="add"
              class="w-full py-2 mt-2 text-white duration-200 bg-green-500 rounded shadow-md hover:bg-green-600"
              type="button"
            >
              Add
            </button>
            <button
              @click="clear"
              class="w-full py-2 mt-2 text-white duration-200 bg-red-500 rounded shadow-md hover:bg-red-600"
              type="button"
            >
              Clear
            </button>
          </div>
        </div>
      </div>
      <div class="grid grid-cols-12 gap-5">
        <div
          v-for="(priceTag, index) in priceTags"
          :key="index"
          class="col-span-3"
        >
          <div class="flex flex-col space-y-3">
            <div class="w-full h-40 p-2 bg-white">
              <div
                class="relative flex flex-col h-full p-3 space-y-2 border-orange-400 border-t-6"
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
          class="col-span-4"
        >
          <div class="flex flex-col space-y-3">
            <div class="w-full p-2 bg-white border-4 border-orange-400 h-36">
              <div class="relative flex flex-col h-full py-4 space-y-2">
                <div class="z-40">
                  <img
                    class="absolute w-16 top-2"
                    src="/img/logo.png"
                    alt="logo"
                  />
                </div>
                <p
                  class="absolute flex items-center text-[0.6rem] font-bold text-gray-800 top-0 right-2"
                >
                  [{{ priceTag.code }}]
                </p>
                <h1
                  class="absolute text-[0.7rem] font-semibold text-gray-800 line-clamp-2 top-8 text-right"
                >
                  {{ priceTag.title }}
                </h1>
                <p
                  class="absolute flex flex-col items-center text-[0.7rem] font-semibold text-gray-800 bottom-2 left-1"
                >
                  <span>PRICE:</span>
                  <span>(Baht)</span>
                </p>
                <h4
                  class="absolute bottom-0 flex items-center text-5xl font-bold text-gray-800 right-1"
                >
                  <span>{{ priceTag.price }}</span>
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

const json = ref(null);

const stage = ref(1);

const code = ref("P-000");

const title = ref(
  "Lorem, ipsum dolor sit amet consectetur adipisicing elit. Vero quod consequuntur ad, obcaecati repellendus accusantium totam harum vel molestiae voluptate, sed maiores quae suscipit corrupti ratione nihil officiis reprehenderit odit."
);
const price = ref(888);

const priceTags = ref([]);

const save = () => {
  priceTags.value.push({
    code: code.value,
    title: title.value,
    price: price.value,
  });

  console.log(priceTags.value);
};

const remove = (index) => {
  priceTags.value.splice(index, 1);
};

const confirm = () => {
  stage.value = 2;
};

const add = () => {
  priceTags.value = priceTags.value.concat(JSON.parse(json.value));
  console.log(priceTags.value);
};

const clear = () => {
  json.value = null;
};

const back = () => {
  stage.value = 1;
};
</script>
