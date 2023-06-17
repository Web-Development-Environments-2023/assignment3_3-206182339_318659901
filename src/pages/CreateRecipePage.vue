<template>
  <div class="container">
    <br/>
    <br/>
    <br/>
    <br/>
    <!-- <h1 class="big-title text-center">Create Recipe</h1> -->
    <RecipePreviewList route_name="/CreateRecipes" title="Create Recipes" class="CreateRecipes center" />
    <br/>
    <br/>
    <b-form @submit.prevent="createRecipe" @reset.prevent="onReset">

      <!-- UserId -->
      <b-form-group 
        id="input-group-user_id"
        label-cols-sm="3"
        label="User ID:"
        label-for="user_id"
        class="user_id-field"
      >
        <div v-if="!$v.form.image.required" class="invalid-feedback">
          Image is required.
        </div>
        <b-form-input
          id="user_id"
          v-model="form.user_id"
          type="text"
          :state="validateState('user_id')"
        ></b-form-input>
      </b-form-group>

      <!-- Image -->
      <b-form-group 
        id="input-group-image"
        label-cols-sm="3"
        label="Image:"
        label-for="image"
        class="image-field"
      >
        <div v-if="!$v.form.image.required" class="invalid-feedback">
          Image is required.
        </div>
        <b-form-input
          id="image"
          v-model="form.image"
          type="text"
          :state="validateState('image')"
        ></b-form-input>
      </b-form-group>

      <!-- Title -->
      <b-form-group 
        id="input-group-title"
        label-cols-sm="3"
        label="Title:"
        label-for="title"
        class="title-field"
      >
        <b-form-input
          id="title"
          v-model = "$v.form.title.$model"
          type="text"
          :state="validateState('title')"
        >
        </b-form-input>
      </b-form-group>

      <!-- ready Minutes -->
      <b-form-group 
        id="input-group-readyInMinutes"
        label-cols-sm="3"
        label="Prepration Time:"
        label-for="readyInMinutes"
        class="readyInMinutes-field"
      >
        <b-form-input
          id="readyInMinutes"
          v-model = "$v.form.readyInMinutes.$model"
          type="text"
          :state="validateState('readyInMinutes')"
        >
        </b-form-input>
      </b-form-group>

      <!-- Gluten Free -->
      <b-form-group 
        id="input-group-glutenFree"
        label-cols-sm="3"
        label="Gluten Free:"
        label-for="glutenFree"
        class="glutenFree-field"
      >
        <b-form-input
          id="glutenFree"
          v-model = "$v.form.glutenFree.$model"
          type="text"
          :state="validateState('glutenFree')"
        >
        </b-form-input>
      </b-form-group>

      <!-- Vegan -->
      <b-form-group 
        id="input-group-vegan"
        label-cols-sm="3"
        label="Vegan:"
        label-for="vegan"
        class="vegan-field"
      >
        <b-form-input
          id="vegan"
          v-model = "$v.form.vegan.$model"
          type="text"
          :state="validateState('vegan')"
        >
        </b-form-input>
      </b-form-group>

      <!-- Vegetarian -->
      <b-form-group 
        id="input-group-vegetarian"
        label-cols-sm="3"
        label="Vegetarian:"
        label-for="vegetarian"
        class="vegetarian-field"
      >
        <b-form-input
          id="vegetarian"
          v-model = "$v.form.vegetarian.$model"
          type="text"
          :state="validateState('vegetarian')"
        >
        </b-form-input>
      </b-form-group>

      <!-- Ingredients -->
      <b-form-group 
        id="input-group-ingredients"
        label-cols-sm="3"
        label="Ingredients:"
        label-for="ingredients"
        class="ingredients-field"
      >
        <b-form-input
          id="ingredients"
          v-model = "$v.form.ingredients.$model"
          type="text"
          :state="validateState('ingredients')"
        >
        </b-form-input>
      </b-form-group>

      <!-- prepInstructions -->
      <b-form-group 
        id="input-group-prepInstructions"
        label-cols-sm="3"
        label="Preperation Instructions:"
        label-for="prepInstructions"
        class="prepInstructions-field"
      >
        <b-form-input
          id="prepInstructions"
          v-model = "$v.form.prepInstructions.$model"
          type="text"
          :state="validateState('prepInstructions')"
        >
        </b-form-input>
      </b-form-group>

      <!-- numberOfDishes -->
      <b-form-group 
        id="input-group-numberOfDishes"
        label-cols-sm="3"
        label="Number Of Dishes:"
        label-for="numberOfDishes"
        class="numberOfDishes-field"
      >
        <b-form-input
          id="numberOfDishes"
          v-model = "$v.form.numberOfDishes.$model"
          type="text"
          :state="validateState('numberOfDishes')"
        >
        </b-form-input>
      </b-form-group>

      <b-button class="btn-primary" type="reset" pill >Reset</b-button>
      <b-button
        pill type="submit"
        class="btn-warning"
        >Create Recipe
      </b-button>
    </b-form>
  </div>
</template>


<script>
  import { minLength } from 'vuelidate/lib/validators';
  import{
    required,
    alpha} from "vuelidate/lib/validators";
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
        },
        validated: false
      };
    },
    validations: {
      form: {
        user_id:{
          required,
          alpha,
          length: (u) => minLength(3)(u) && maxLength(8)(u),
        },
        image: {
          required,
          alpha
        },
        title: {
          required,
          alpha
        },
        readyInMinutes: {
          required,
          alpha
        },
        glutenFree: {
          required,
          alpha
        },
        vegan: {
          required,
          alpha
        },
        vegetarian: {
          required,
          alpha
        },
        image: {
          required,
          alpha
        },
        ingredients: {
          required,
          alpha
        },
        prepInstructions: {
          required,
          alpha

        },
        numberOfDishes: {
          required,
          digit: (p) => p && /\d/.test(p), 
          
        },
      }
    },
    components:{
      RecipePreviewList
    },
    methods: {
      async createRecipe(){
        this.$v.form.$touch();
        if (this.$v.form.$anyError) {
          return;
        }
        try{
          const response = await this.axios.post(
            this.$root.store.server_domain + "/users/MyRecipes",
            {
              user_id: this.form.user_id,
              recipePreview: {
                image: this.form.image,
              title: this.form.title,
              readyInMinutes: this.form.readyInMinutes,
              glutenFree: this.form.glutenFree,
              vegan: this.form.vegan,
              vegetarian: this.form.vegetarian,
             
            },
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
      },
      validateState(param) {
      const { $dirty, $error } = this.$v.form[param];
      return $dirty ? !$error : null;
    }
    }
  }
</script>

<style>
</style>
