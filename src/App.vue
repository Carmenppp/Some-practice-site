<script setup>
import { ref, onMounted } from 'vue';
import LoaderSpinner from './components/LoaderSpinner.vue'
import PaginatePost from './components/PaginatePost.vue'
import BlogPost from './components/BlogPost.vue';


const posts = ref([]);
const postxpage = 10
const inicio = ref(0)
const fin = ref(postxpage)
const loading = ref(true)

const favorito = ref('')

const cambiarFavorito = (title) => {
  favorito.value = title;
}

const next = () => {
  inicio.value = inicio.value + postxpage;
  fin.value = fin.value + postxpage;
}

const previous = () => {
  inicio.value += - postxpage;
  fin.value += - postxpage;
}

onMounted(async() => {
 // loading.value = true;
  try {
   const res = await fetch('https://jsonplaceholder.typicode.com/posts')
   posts.value = await res.json()
  } catch (error) {
    console.log(error)
  } finally {
    setTimeout (() => {
        loading.value = false;
        }, 2000);

  }
  
})
//fetch('https://jsonplaceholder.typicode.com/posts')
    // .then(res => res.json())
    //  .then(data => posts.value = data)
     // .catch(e => console.log(e))
     // .finally(() => {
      //  setTimeout (() => {
      //    loading.value = false;
      //  }, 2000);
      //});

</script>

<template>
  <LoaderSpinner v-if="loading"></LoaderSpinner>
  <div class="container" v-else>
   
  <h1>APP</h1>
  <h2>Mi post favorito: {{ favorito }}</h2>
  
  
  <PaginatePost 
  class="mb-2" @previous="previous" @next="next" :inicio="inicio" :fin="fin" :maxLength="posts.length"
  ></PaginatePost>
  <BlogPost 
  v-for="post in posts.slice(inicio, fin)"
      :key="post.id"
      :title="post.title" 
      :id= "post.id"
      :body="post.body"
      @cambiarFavoritoNombre = "cambiarFavorito"
      class="mb-2"
  ></BlogPost>
 
</div>
</template>