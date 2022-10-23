<script setup>
import { ref, computed } from "vue";

import Posts from "./components/Posts.vue";
import Paginacion from "./components/Paginacion.vue";
import Spinner from "./components/Spinner.vue";

// -------------------------POSTS----------------------------

const postsArray = ref([]);

fetch("https://jsonplaceholder.typicode.com/posts")
  .then((res) => res.json())
  .then((data) => {
    postsArray.value = data;
  })
  .finally(() => {
    setTimeout(() => {
      loading.value = false
    },2000)
  });

  // .finally(() => (loading.value = false ));

// -------------------------FAVORITO----------------------------

const PostFaborito = ref("");
postsArray;

const CambiarFavorito = (postNum) => {
  PostFaborito.value = postNum;
};

// ------------------NUMERO POSTS-------------------------------
const PostsXPagina = 10;
const NumInicio = ref(0);
const NumFin = ref(PostsXPagina);

const maxLength = computed(() => postsArray.value.length);



// ------------------------BOTONES------------------------------

const siguiente = () => {
  // NumInicio.value = NumInicio.value + PostsXPagina;
  // NumFin.value = NumFin.value + PostsXPagina;

  (NumFin.value >= maxLength.value) ? NumInicio.value = 0 : NumInicio.value = NumInicio.value + PostsXPagina;
  (NumFin.value >= maxLength.value) ? NumFin.value = 10 : NumFin.value = NumFin.value + PostsXPagina;

};

const retroceder = () => {
  // NumInicio.value = NumInicio.value - PostsXPagina

  // NumInicio.value += -PostsXPagina;
  // NumFin.value += -PostsXPagina;

  if(NumInicio.value <= 0) { 
    NumInicio.value = maxLength.value - 10 
    NumFin.value = maxLength.value
  }else{
    NumInicio.value += -PostsXPagina
    NumFin.value += -PostsXPagina
  }

};

// --------------------------SPINNER----------------------------------

const loading= ref(true)
</script>

<template>
  <Spinner v-if="loading"/>
  <div class="container" v-else>
    <div class="row">
      <div class="col-12 text-center">
        <h1>POSTS</h1>
      </div>
      <div class="col-12">
        <h2>Post Favorito: {{ PostFaborito }}</h2>
      </div>
      <div class="col-12">
        <Paginacion
          class="my-2"
          @sgt="siguiente"
          @rtn="retroceder"
          :Inicio="NumInicio"
          :Fin="NumFin"
          :maxLength=maxLength
        />
      </div>
      <div class="col-12 mt-2">
        <Posts
          v-for="post in postsArray.slice(NumInicio, NumFin)"
          :key="post.id"
          :title="post.title"
          :id="post.id"
          :body="post.body"
          @CambiarFavoritoFetch="CambiarFavorito"
          class="mb-2"
        >
        </Posts>
      </div>
    </div>
  </div>
  <HelloWorld msg="Posts" />
</template>

<style scoped></style>
