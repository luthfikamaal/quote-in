<template>
  <button @click="getQuote" class="fixed right-3 bottom-3 rounded-md bg-indigo-600 px-3 py-2 text-white">
    <i class="bi bi-arrow-clockwise"></i>
  </button>
  <div class="bg-hero">
    <div class="h-screen bg-black/40">
      <div class="flex h-screen items-center justify-center px-6">
        <div class="block w-full md:w-1/2">
          <p class="font-quote mb-2 text-4xl text-white shadow-sm">{{ quote.quote }}</p>
          <div class="font-author text-xl text-white">- {{ quote.author }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import urlAPI from '@/api/config.js';
export default {
  data() {
    return {
      name: 'Muhammad Luthfi Kamal',
      quote: {
        quote: 'Loading...',
      },
    };
  },
  methods: {
    getQuote() {
      this.quote = {
        quote: 'Loading...',
      };
      axios
        .get(urlAPI)
        .then((result) => {
          this.quote = result.data;
        })
        .catch((err) => {
          console.log(err.message);
        });
    },
  },
  setup() {
    let quote = ref({});
    onMounted(() => {
      axios
        .get(urlAPI)
        .then((result) => {
          quote.value = result.data;
        })
        .catch((err) => {
          console.log(err.message);
        });
    });
    return {
      quote,
    };
  },
};
</script>
