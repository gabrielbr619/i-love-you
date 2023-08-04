<template>
  <div class="hello">
    <h1>ei garota, <br>eu te amo</h1>
    <div class="container">
      <button class="btn btn-primary btn-lg" @click="showRandomRecipe">Quer ver uma receita aleatória?</button>
    </div>
    <RecipePage v-if="shouldShowRecipe" :recipe="currentRecipe" :key="currentRecipe._id.$oid" />
  </div>
</template>

<script>
import RecipePage from './Recipe.vue'; // Importe o componente Recipe
import recipesData from '@/assets/recipes.json';

export default {
  name: 'ButtonWithRecipe',
  components: {
    RecipePage, // Registre o componente Recipe para ser usado no template
  },
  data() {
    return {
      shouldShowRecipe: false,
      currentRecipe: null,
      recipes: recipesData, // Adicione a propriedade 'recipes' para guardar os dados das receitas
    };
  },
  methods: {
    showRandomRecipe() {
      const randomIndex = Math.floor(Math.random() * this.recipes.length);
      this.currentRecipe = this.recipes[randomIndex];
      if (!this.currentRecipe.secao.some((secao) => secao.nome === ' Ingredientes' && secao.conteudo.length > 1)) {
        this.showRandomRecipe();
      }

      this.currentRecipe.secao.forEach((secao) => {
        secao.conteudo = this.removeEmptyStrings(secao.conteudo);
      });

      this.shouldShowRecipe = true; // Ative a renderização do componente Recipe ao clicar no botão
    },
    removeEmptyStrings(arr) {
      return arr.filter((item) => item.trim() !== "");
    },
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

a {
  color: #42b983;
}
</style>
