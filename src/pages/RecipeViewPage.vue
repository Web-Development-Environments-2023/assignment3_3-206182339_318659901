<template>
  <center>
    <br/>
    <br/>
  <div class="recipe-footer">
    <h4 id="big-title" :title="recipe.recipePreview.title" class="recipe-title">
      {{ recipe.recipePreview.title }}
    </h4>
    <h4 id= "family-title" v-if="is_family"> This recipe was made with love by {{ recipe.familyMember }} and we used to make it on {{recipe.familyTime}} .</h4>
    <br/>
    <div pill class="recipe-body">
        <!-- <img v-if="image_load" :src="recipe.image" class="recipe-image" /> -->
        <img :src="recipe.recipePreview.image" style="height:500px; width:600px;" class="recipe-image" />
    </div>
    <br/>
    <ul class="recipe-overview">
      <b-list-group >
        <dt>  ⏰ {{ recipe.recipePreview.prepTime }} minutes to prepare</dt>
        <dt> 🍲 {{ recipe.numberOfDishes }} servings</dt>
        <dt> ❤️ {{ recipe.recipePreview.popularity }}  liked this recipe</dt>
        <dt v-if="recipe.recipePreview.vegan"> 🌿🌿 Vegan</dt>
        <dt v-if="recipe.recipePreview.vegetarian">🌿 Vegeterian</dt>
        <dt v-if="recipe.recipePreview.glutenFree">🌾🚫  Gluten Free</dt>
        <dt v-if="recipe.recipePreview.Favorite">💗 Favorite Recipe</dt>
        <dt v-if="recipe.recipePreview.Seen"> 👁️ Viewed Recipe</dt>
        <br/>
       <center>
           <b-button pill v-if="API_route" id="favoritesButton" size="sm" @click="AddToFavorites" class="btn-warning w-15 h-20"> Add to favorites 💗</b-button>
        </center>
      </b-list-group >
      <!-- extendedIngredients -->
       <br/>
      <h5 id="IngredientsTitle">Ingredients</h5> <br/>
      <b-col>
      <center>
        <div> {{ recipe.ingredients }} </div>
      <!-- <div v-for="ing in recipe.ingredients" :key="ing.name">
        {{ing.amount }} {{ing.name }}
      </div> -->
      </center>
      <br/>
      <div id="instructions" > <h5 id="InstructionsTitle">Instructions</h5> <br/>
         {{ instructions }}</div>
         </b-col>
    </ul>
</div>
</center>
</template>

<script>
// import RecipePreview from "./RecipePreview.vue";
export default {
name: "Recipeview",
data() {
  return {
    recipe: {},
    instructions:"",
    recipe_id:"",
    API_route: false,
    is_family : false,
  };
},
mounted() {
  this.updateRecipes();
},
methods: {
  async updateRecipes() {

    try {
      let split_route = (((this.$route.path).split("/")[2]).split("%2F"))[2]
      let split_recipe_id = ((this.$route.path).split("/"))[4]
      console.log(this.$route.path)

       if(split_route == "lastViewedRecipes" || split_route =="randomRecipes" || split_route =="favorites" || split_route =="search"){
        this.API_route = true;
        const response = await this.axios.get(
        this.$root.store.server_domain + "/recipes/ExtendedRecipes/" + split_recipe_id  + "?isMyRecipe=false"
      
        );
        this.instructions = response.data.prepInstructions
   
      this.recipe= response.data;
      this.recipe_id= response.data.recipePreview.id;    
     
      }
      if (split_route == "MyRecipes"){
        const response = await this.axios.get(
        this.$root.store.server_domain + "/recipes/ExtendedRecipes/" + split_recipe_id + "?isMyRecipe=true"
        
        );
        this.instructions = response.data.prepInstructions
   
      this.recipe= response.data;
      this.recipe_id= response.data.recipePreview.id; 
      }
      if (split_route == "familyRecipes"){
        const response = await this.axios.get(
        this.$root.store.server_domain + "/recipes/ExtendedRecipes/" + split_recipe_id + "?isMyRecipe=true"
        
        );
        
        this.instructions = response.data.prepInstructions
   
      this.recipe= response.data;
      this.recipe_id= response.data.recipePreview.id; 
      this.is_family=true;
      }
      // else{
      //   // console.log("else:")
      //   const response = await this.axios.get(
      //   this.$root.store.server_domain + "/users/FullRecipeDetailsDB/" + split_recipe_id)
      //   // console.log(response);

      //   this.recipe= response.data[0];
      //   if(split_route=="familyRecipes"){
      //     console.log(this.recipe.title.replace('family-',''))
      //     this.recipe.title = this.recipe.title.replace('family-','')
      //   }
      //   this.instructions = response.data[0].instructions;
      //   this.recipe_id= response.data[0].id;
      // }
   
    } catch (error) {
      console.log(error);
    }
  },
 
  async AddToFavorites(){
     const response = await this.axios.post(
        // "https://test-for-3-2.herokuapp.com/user/Register",
        this.$root.store.server_domain + "/users/favorites",
        {
          recipeId: this.recipe_id
        }
      );
      window.location.reload();

  }
},
// computed: {
//     formattedInstructions() {
//       const lines = this.instructions.split("\n");
//       return lines.map((line, index) => {
//         return `<p>${index + 1}. ${line}</p>`;
//       }).join("");
//     },
//   },
};
</script>

<style scoped>
.favoritesButton{
background-color:  #06467a;
color: #0ad8d8;
}
.recipe-title{
  color: #2f4f4f;
font-weight: bolder;
font-size: 32px;

}
.recipe-overview{
font-size: 20px;
}
#InstructionsTitle{

  font-family:"Papyrus";
  color:#0f4e9f; 
  text-shadow: -1px 0 black, 0 3px black, 1px 0 black, 0 -1px black;
  font-size: 48px;
font-weight: bolder;
}
#IngredientsTitle{

  font-family:"Papyrus";
  color:#0f4e9f; 
  text-shadow: -1px 0 black, 0 3px black, 1px 0 black, 0 -1px black;
  font-size: 48px;
font-weight: bolder;
}
#instructions{
max-width: 800px; 
width:800px; 
}
.btn-warning{
 background-color: #9cbef1;
 border-color: #9cadf1;
 width:200px;font-weight: bold;color: #080807;
}
.recipe-footer {
  background: #c0e4f4;
  background: -moz-linear-gradient(-45deg, #4364f7 0%, #8a9af9 53%, #c0e4f4 100%);
  background: -webkit-linear-gradient(-45deg, #4364f7 0%, #8a9af9 53%, #c0e4f4 100%);
  background: linear-gradient(135deg, #4364f7 0%, #8a9af9 53%, #c0e4f4 100%);
  max-width: 1000px;
  width: 1000px;
  padding: 1em;
}

#big-title{

  font-family:"Papyrus";
  color:#0f4e9f; 
  text-shadow: -1px 0 black, 0 3px black, 1px 0 black, 0 -1px black;
  font-size: 48px;
  font-weight: bolder;
}
#family-title{
  font-family:"Papyrus";
  color:#e38cb3; 
 
  font-weight: bolder;
}

</style>