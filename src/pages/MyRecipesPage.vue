<template>
    <div class="container">
        <br/>
        <br/>
        <br/>
        <br/>
        <RecipePreviewList route_name="/users/MyRecipes" title="My Recipes" class="MyRecipes center" />
        <br/>
        <br/>
    </div>
</template>


<script>
import RecipePreviewList from "../components/RecipePreviewList";
export default {
    name : "myRecipes",
    components:{
        RecipePreviewList   
    },
    methods: {
    //TODO add methods.
    }
};
</script>

<style lang="scss" scoped>

</style>
