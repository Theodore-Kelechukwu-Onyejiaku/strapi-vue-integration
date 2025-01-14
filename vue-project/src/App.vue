<template>
  <div class="p-6">
    <h1 class="text-4xl font-bold mb-8">Vue.js and Strapi Integration</h1>
    <div>
      <h2 class="text-2xl font-semibold mb-6">Articles</h2>
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <article
          v-for="article in articles"
          :key="article.id"
          class="bg-white shadow-md rounded-lg overflow-hidden"
        >
          <img
            :src="STRAPI_URL + article.cover.url"
            alt="Article Image"
            class="w-full h-48 object-cover"
          />
          <div class="p-4">
            <h3 class="text-lg font-bold mb-2">{{ article.title }}</h3>
            <p class="text-gray-600 mb-4">{{ article.content }}</p>
            <p class="text-sm text-gray-500">
              Published: {{ formatDate(article.publishedAt) }}
            </p>
          </div>
        </article>
      </div>
    </div>
  </div>
</template>

<script setup>
// Import dependencies
import { ref, onMounted } from "vue";

// Variables
const articles = ref([]);

// Strapi Base URL
const STRAPI_URL = "http://localhost:1337" || import.meta.env.VITE_STRAPI_URL;

// Fetch articles
const getArticles = async () => {
  const response = await fetch(`${STRAPI_URL}/api/articles?populate=*`);
  const data = await response.json();
  articles.value = data.data;
};

// Format date
const formatDate = (date) => {
  const options = { year: "numeric", month: "2-digit", day: "2-digit" };
  return new Date(date).toLocaleDateString("en-US", options);
};

// Fetch articles on component mount
onMounted(() => {
  getArticles();
});
</script>
