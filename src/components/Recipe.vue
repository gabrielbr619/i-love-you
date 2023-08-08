<template>
  <div v-if="recipe">
    <h1 style="font-weight: bolder;">{{ recipe.nome }}</h1>
    <img :src="thumbnailUrl">
    <div v-for="secao in recipe.secao" :key="secao.nome">
      <h2>{{ secao.nome }}</h2>
      <ul>
        <li class="list-item" v-for="item in secao.conteudo" :key="item">{{ item }}</li>
      </ul>
    </div>
  </div>
  <div v-else>
    <p>Nenhuma receita encontrada</p>
  </div>
</template>

<script>
// import axios from 'axios';

export default {
  name: 'RecipePage',
  props: {
    recipe: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      thumbnailUrl: '',
    };
  },
  created() {
    this.fetchThumbnail();
  },
  methods: {
    async fetchThumbnail() {
      try {
        // const response = await axios.get('https://get-recipe-images.onrender.com/get-recipe-thumbnail', {
        //   params: {
        //     name: this.recipe.nome,
        //   },
        // });

        this.thumbnailUrl = "response.data.thumbnailUrl";
        console.log(this.thumbnailUrl)
      } catch (error) {
        console.log('Erro ao obter a URL da imagem:', error);
      }
    },
  },
};
</script>

<style scoped>

h1{
  padding: 0 15px;
}

ul {
  list-style: none;
  padding: 0 15px; 
}

li {
  margin-top: 10px;
}
</style>




