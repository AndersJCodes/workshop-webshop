<script setup lang="ts">
import { ref, provide } from 'vue';
import { RouterView } from 'vue-router';
import { useFetch } from './services/fetch';

import TheHeader from './components/TheHeader.vue';
import HeroProducts from './components/HeroProducts.vue';

import { useUserStore } from './stores/userStore';
import { storeToRefs } from 'pinia';

const userStore = useUserStore();
const { name } = storeToRefs(userStore);
provide('user', name);

const message = ref('hello');
const { data, error } = useFetch('https://fakestoreapi.com/products');
</script>

<template>
  <header>
    <TheHeader />
  </header>

  <main>
    <p>home{{ $route.fullPath }}</p>
    <h1>{{ message }}</h1>

    <HeroProducts :products="data" />

    <RouterView />
  </main>
</template>

<style scoped>
.hero-products {
  padding: 1rem 0;
}

.product-card {
  margin: 2rem 0;
}
</style>
