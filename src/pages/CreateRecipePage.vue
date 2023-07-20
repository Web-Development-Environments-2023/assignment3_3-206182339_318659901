<template>
  <div class="container">
    <br/>

    <div id="create-recipe-modal-content">
        <b-modal id="modal-1" header-bg-variant="info" ref="my-modal" title="Create New Recipe" hide-footer>
    <b-form @submit.prevent="createRecipe" @reset.prevent="onReset">
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
          placeholder = "image url"
        ></b-form-input>
      </b-form-group>

      <!-- Title -->
      <b-form-group 
        id="input-group-title"
        label-cols-sm="3"
        label="Recipe name:"
        label-for="title"
        class="title-field"
      >
        <b-form-input
          id="title"
          v-model = "$v.form.title.$model"
          type="text"
          :state="validateState('title')"
          placeholder = "Enter recipe name"
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
          placeholder = "Enter prepration time in minutes.."
        >
        </b-form-input>
      </b-form-group>

      <b-form-checkbox v-model="$v.form.glutenFree.$model" name="check-button1" switch>
        Gluten free?
    </b-form-checkbox>       
    <b-form-checkbox v-model="$v.form.vegan.$model" name="check-button2" switch>
        Vegan? 
    </b-form-checkbox>
    <b-form-checkbox v-model="$v.form.vegetarian.$model" name="check-button3" switch>
        Vegetarian? 
    </b-form-checkbox>  

      <!-- Ingredients -->
      <b-form-group 
        id="input-group-ingredients"
        label-cols-sm="3"
        label="Ingredients:"
        label-for="ingredients"
        class="ingredients-field"
      >
        <b-form-textarea
          id="ingredients"
          v-model = "$v.form.ingredients.$model"
          type="text"
          :state="validateState('ingredients')"
          placeholder = "Enter recipe ingredients. for example: oil- 2 cups | sugar- 1 cup |..."
          rows="4"
        >
        </b-form-textarea>
      </b-form-group>

      <!-- prepInstructions -->
      <b-form-group 
        id="input-group-prepInstructions"
        label-cols-sm="3"
        label="Preperation Instructions:"
        label-for="prepInstructions"
        class="prepInstructions-field"
      >
        <b-form-textarea
          id="prepInstructions"
          v-model = "$v.form.prepInstructions.$model"
          type="text"
          :state="validateState('prepInstructions')"
          placeholder = "Enter recipe Instructions. for example: 1.mix the ingredients into bowl. 2.make small balls.."
          rows="4"
        >
        </b-form-textarea>
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
          placeholder = "Enter number of servings.."
        >
        </b-form-input>
      </b-form-group>

      <b-button class="btn-primary" type="reset" pill >Reset</b-button>
      <b-button
        pill type="submit"
        class="btn-info"
        >Create Recipe
      </b-button>
    </b-form>
</b-modal>
</div>
  </div>
</template>


<script>
  import { BModal } from 'bootstrap-vue';
  import { minLength } from 'vuelidate/lib/validators';
  import{
    required,
    alpha} from "vuelidate/lib/validators";
  import RecipePreviewList from "../components/RecipePreviewList";
  export default {
    // name : "Create Recipes",
//     components: {
//     BModal
//   },
    data(){
      return{
        form:{
          image: "",
          title: "",
          readyInMinutes: "",
          glutenFree: false,
          vegan: false,
          vegetarian: false,
          ingredients: "",
          prepInstructions: "",
          numberOfDishes: "",
        },
        validated: false
      };
    },
    validations: {
      form: {
        image: {
          required,
        
        },
        title: {
          required,
         
        },
        readyInMinutes: {
          required,
          digit: (p) => p && /\d/.test(p), 
        },
        glutenFree: {
          required,
         
        },
        vegan: {
          required,
        
        },
        vegetarian: {
          required,
         
        },
       
        ingredients: {
          required,
          
        },
        prepInstructions: {
          required,
         

        },
        numberOfDishes: {
          required,
          digit: (p) => p && /\d/.test(p), 
          
        },
      }
    },
    // components:{
    //   RecipePreviewList
    // },
  
    methods: {
      async createRecipe(){
        this.$v.form.$touch();
        if (this.$v.form.$anyError) {
          return;
        }
        try{
          const user_id = await this.axios.get(
          this.$root.store.server_domain + "/users/userid"
        );
          const response = await this.axios.post(
            this.$root.store.server_domain + "/users/MyRecipes",
            {
              user_id: user_id.data,
              recipePreview:{
                image: this.form.image,
                title: this.form.title,
                readyInMinutes: this.form.readyInMinutes,
                glutenFree: this.form.glutenFree & 1,
                vegan: this.form.vegan & 1,
                vegetarian: this.form.vegetarian & 1,
              },
              ingredient: this.form.ingredients,
              prepInstructions: this.form.prepInstructions,
              numberOfDishes: this.form.numberOfDishes,
              }
            
            
          );
        //   // move to My Recipe Page
        //   this.$router.push("/MyRecipes");
        await this.onReset();
        this.$refs['my-modal'].hide()
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
          glutenFree: false,
          vegan: false,
          vegetarian: false,
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
