<template>
  <div class="hello">
    <h1>ei garota, <br>eu te amo</h1>
    <div class="container">
      <button class="btn btn-primary btn-lg" @click="showRandomRecipe">Quer ver uma receita aleatória?</button>
      <button class="btn btn-primary btn-lg" @click="showRandomPicture">Quer me ver?</button>
    </div>
    <RecipePage v-if="shouldShowRecipe" :recipe="currentRecipe" :key="currentRecipe._id.$oid" />
    <PicturePage v-if="shouldShowPicture" />
  </div>
</template>

<script>
import RecipePage from './Recipe.vue'; 
import PicturePage from "./Picture.vue";
import recipesData from '@/assets/recipes.json';


export default {
  name: 'ButtonWithRecipe',
  components: {
    RecipePage,
    PicturePage
  },
  data() {
    return {
      shouldShowRecipe: false,
      shouldShowPicture: false,
      currentRecipe: null,
      recipes: recipesData, 
    };
  },
  methods: {
    showRandomRecipe() {
      const randomIndex = Math.floor(Math.random() * this.recipes.length);
      this.currentRecipe = this.recipes[randomIndex];
      if (this.isSecaoEmpty(this.currentRecipe)) {
        this.showRandomRecipe();
      }

      this.currentRecipe.secao.forEach((secao) => {
        secao.conteudo = this.removeEmptyStrings(secao.conteudo);
      });
      console.log(this.currentRecipe)
      this.souldShowPicture = false;
      this.shouldShowRecipe = true; 
    },
    showRandomPicture() {
      this.shouldShowRecipe = false;
      this.shouldShowPicture = true;
    },
    removeEmptyStrings(arr) {
      return arr.filter((item) => item.trim() !== "");
    },
    isSecaoEmpty(currentRecipe) {
      const hasIngredients = currentRecipe.secao.some((secao) => secao.nome === ' Ingredientes' && secao.conteudo.length > 1)
      const hasCookingSteps = currentRecipe.secao.some((secao) => secao.nome === ' Modo de Preparo' && secao.conteudo.length > 1)

      if(hasIngredients && hasCookingSteps) return false;

      return true
    }
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

button{ 
  margin: .5em 0;
}

.container{
  margin: 2em 0;
  display: flex;
  flex-direction: column;
}

a {
  color: #42b983;
}
</style>
