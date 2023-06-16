<template>
        <div class="container">
      <br/>
      <br/>
      <br/>
      <br/>
      <RecipePreviewList route_name="/users/MyRecipes" title="My Recipes" class="MyRecipes center" />
      <br/>
      <br/>
      <b-form @submit.prevent="createRecipe" @reset.prevent="onReset">
      <b-form-group 
        id="input-group-image"
        label-cols-sm="3"
        label="Image:"
        label-for="image"
        class="image-field"
      >
        <b-form-input
          id="image"
          v-model = "$v.form.image.$model"
          type="text"
        >
        </b-form-input>
      </b-form-group>


      </b-form>
  </div>
</template>


<script>
import RecipePreviewList from "../components/RecipePreviewList";
export default {
  name : "Create Recipes",
  data(){
    return{
      form:{
        user_id: "",
        image: "",
        title: "",
        readyInMinutes: "",
        glutenFree: "",
        vegan: "",
        vegetarian: "",
        ingredients: "",
        prepInstructions: "",
        numberOfDishes: "",
      }
    };
  },
  components:{
    RecipePreviewList
  },
  methods: {
    
    async createRecipe(){
      try{
        const response = await this.axios.post(
          this.$root.store.server_domain + "/MyRecipes",
          {
            user_id: this.form.user_id,
            image: this.form.image,
            title: this.form.title,
            readyInMinutes: this.form.readyInMinutes,
            glutenFree: this.form.glutenFree,
            vegan: this.form.vegan,
            vegetarian: this.form.vegetarian,
            ingredients: this.form.ingredients,
            prepInstructions: this.form.prepInstructions,
            numberOfDishes: this.form.numberOfDishes,
          }
        );
        // move to My Recipe Page
        this.$router.push("/MyRecipes");
      } catch (err) {
        console.log(err.response);
        this.form.submitError = err.response.data.message;
      }
    },
    onReset() {
      this.form = {
        user_id: "",
        image: "",
        title: "",
        readyInMinutes: "",
        glutenFree: "",
        vegan: "",
        vegetarian: "",
        ingredients: "",
        prepInstructions: "",
        numberOfDishes: "",
      };
      this.$nextTick(() => {
        this.$v.$reset();
      });
    }
  }
}
</script>

<style>
</style>