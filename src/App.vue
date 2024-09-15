<template>
  <div>
    <h1>Deus no comando</h1>
    <h1>Dados da API</h1>
    <div v-for="item in items" :key="item.id" class="item">
      <h2>{{ item.title }}</h2>
      <img :src="'https://image.tmdb.org/t/p/w200'+item.poster_path" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
var access_token = 'eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJhYTExYjg5ZWU5NDczZWI3OGI5YjI2OWZjMjRiMzYzMiIsInN1YiI6IjYxODVjYzY0MDc1Mjg4MDAyODdlYTVmYiIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.0bICTq0SqShQGdpbeyZGflikn9mAe0-h2BeE35I9RYU';
var url ="https://api.themoviedb.org/3/search/multi?query=$popular&include_adult=true&language=en-US&page=5"
export default {
  data() {
    return {
      items: [],
    };
  },
  created() {
    this.fetchItems();
  },
  methods: {
    async fetchItems() {
      try {
        const response = await axios.get(url, {
          headers: {
            'Authorization': `Bearer ${access_token}`
          }
        }); // Substitua pela URL da sua API
        this.items = response.data['results'];
      } catch (error) {
        console.error('Erro ao buscar itens:', error);
      }
    },
  },
};
</script>

<style scoped>
img {
  width: 600px;
  /* Ajuste o tamanho conforme necessário */
  height: auto;
  margin: 10px;
}
</style>
