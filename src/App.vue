<template>
  <div id="app">
    <NavBar/>
    
    <router-view />
  </div>
</template>

<script>
import Search from "../src/pages/SearchPage.vue"
import CreateRecipePage from './pages/CreateRecipePage.vue';
import NavBar from "./components/NavBar.vue";
export default {   
  name: "App",
  components: {
    NavBar,
  },

  methods: {
    Logout() {
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    },
    isLoggedIn(){return $root.store.username;},

  }
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background: url("./assets/tomatoes-tomatoes-lemon-leaves-garlic-bottle-oil-tree-branches.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}
#app::after{
  background-image: url("./assets/tomatoes-tomatoes-lemon-leaves-garlic-bottle-oil-tree-branches.jpg");
  background-repeat: no-repeat;
  background-size: cover;
}

// #nav {
//   padding: 30px;
//     letter-spacing: 2px;
//     color: white;
//     font-size: 30px;
//     font-weight: 50;
//     border: 2px solid #ccd5d9;
//     background-color:rgb(112, 147, 216);
//     padding: 10px 10px;
//     cursor: pointer;
//     border-radius: 10px;
//     animation: fadeIn 1s ease-in forwards;
// }

// #nav a {
//   font-weight: bold;
//   color: #2c3e50;
// }

// #nav a.router-link-exact-active {
//   color:rgb(112, 185, 216);
// }


// .displayUser {
//     color: rgb(112, 143, 216);
//     margin-left: auto;
//     width: 10%;
//     padding: 10px;
//     background-color: #f8f9fa;
//     text-align: right;
//   }
</style>
