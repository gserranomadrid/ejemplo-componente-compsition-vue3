<script setup>
import { ref, computed, onMounted } from "vue";

import BlogPost from "./components/BlogPost.vue";
import ButtonCounter from "./components/ButtonCounter.vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]);
const postsXpage = 10;
const inicio = ref(0);
const fin = ref(postsXpage);
const loading = ref(true);
const favorito = ref("");

const cambiarFavorito = (title) => {
  favorito.value = title;
};

const next = () => {
  inicio.value = inicio.value + postsXpage;
  fin.value = fin.value + postsXpage;
};

const previus = () => {
  inicio.value = inicio.value - postsXpage;
  fin.value = fin.value - postsXpage;
};

const maxLength = computed(() => posts.value.length);

// onMounted(async () => {
//   loading.value = true;
//   try {
//     const res = await fetch("https://jsonplaceholder.typicode.com/posts");
//     posts.value = await res.json();
//   } catch (error) {
//     console.log(error);
//   } finally {
//     setTimeout(() => {
//       loading.value = false;
//     }, 2000);
//   }
// });

// fetch("https://jsonplaceholder.typicode.com/posts")
//   .then((res) => res.json())
//   .then((data) => {
//     posts.value = data;
//   })
//   .finally(() => {
//     setTimeout(() => {
//       loading.value = false;
//     }, 2000);
//   });


// onMounted(async () => {
//fetchData();
// });

const fetchData = async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      loading.value = false;
    }, 2000);
  }
};
fetchData();

</script>
<template>
  <div class="container">
    <LoadingSpinner v-if="loading" />
    <div class="row" v-else>
      <h1>APP</h1>
      <h2>Mi Post Favorito: {{ favorito }}</h2>

      <PaginatePost
        @next="next"
        @previus="previus"
        :inicio="inicio"
        :fin="fin"
        :maxLength="posts.length"
        class="mb-2"
      />

      <BlogPost
        v-for="post in posts.slice(inicio, fin)"
        :title="post.title"
        :id="post.id"
        :body="post.body"
        :cambiarFavorito="cambiarFavorito"
        class="mb-2"
      />
    </div>
  </div>
</template>
