<template>
  <router-link
     :to="{ name: 'recipe', params: { recipeId: recipe.id, route_name: route_name} }" class="recipe-preview">
   
 <div>
  <b-card 
  pill
  class="recipePreviewDetails" 
  :img-src="recipe.image"
  img-alt="Image"
  img-height="400"
  img-width="100"
  img-top
  tag="article"
  style="max-width: 33rem;"
>
  <b-card-title 
    style="font-size: 28px; color: #333; font-weight: bold; font-family: 'Arial', sans-serif;" 
    class="text-center"
  >
    {{ recipe_title }}
  </b-card-title>
  <b-card-text class="recipePreviewDetailsText">
    <b-list-group>
         <!-- <dt style="color: #14b8a6" v-if="is_family">This dish usually prepared by {{ recipe.family_member }} </dt>
         <dt style="color: #14b8a6" v-if="is_family">Traditionally, the dish is prepared {{ recipe.when_prepering }}  </dt> -->
         <dt>    {{ recipe.readyInMinutes }} minutes to prepare</dt>
         <dt>{{ recipe.popularity }}  liked this recipe</dt>
         <dt v-if="recipe.vegan">  Vegan</dt>
         <dt v-if="recipe.vegetarian">Vegeterian</dt>
         <dt v-if="recipe.glutenFree"> Gluten Free</dt>
         <dt v-if="API_route && recipe.Favorite">  Favorite Recipe</dt>
         <dt v-if="API_route && recipe.Seen">  Viewed Recipe</dt>
       </b-list-group>
     </b-card-text>
   </b-card>
 </div>
 </router-link>
 </template>
 
 <script>
 export default {
 
   data() {
     return {
        API_route: false,
        is_family: false,
        recipe_title: ""
       //  split_route: ""
     };
   },
   props: {
     recipe: {
       type: Object,
       required: true
     },
     title: {
       type: String,
       required: true
     },
     route_name:{
       type: String,
       required: true
     },
   },
   
 mounted() {this.updateRecipes(),
 this.recipe_title= this.recipe.title.replace('family-','')},
  methods: {
     async updateRecipes() {
       try {
           // console.log("rout.path:  " + this.$route.path)
           // if(this.split_route=="" ||split_route == "lastWatched" || split_route =="random" || split_route =="favorites" || split_route =="search"){
           if(this.$route.path=="/" ||this.$route.path == "/lastViewedRecipes" || this.$route.path =="/randomrecipes" || this.$route.path =="/users/favorites" || this.$route.path =="/search"){
             this.API_route = true;
           }
           else if(this.$route.path=="/users/familyRecipes"){
               this.is_family = true;
 
           }
       }catch (error) {
           console.log(error);
       }
     }
   }
   
 };
 </script>
 
 <style scoped>
 .recipePreviewDetails{
   
   background-color: #C4FAF8;
   border-radius:30px;
   /* background-color: rgb(251, 248, 157); */
 }
 .recipePreviewDetailsText{
   color: black;
   
 }
 </style>