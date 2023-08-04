<template>
  <div v-if="recipe">
    <h1 style="font-weight: bolder;">{{ recipe.nome }}</h1>
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
export default {
  name: 'RecipePage',
  props: {
    recipe: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>

ul {
  list-style: none;
  padding: 0 15px; 
}

li {
  margin-top: 10px;
}
</style>
