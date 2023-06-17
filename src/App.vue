<template>
  <div id="app">
    <div id="nav">
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container">
          <div class="navbar-collapse">
            <ul class="navbar-nav me-auto">
              <li class="nav-item">
                <router-link class="nav-link" :to="{ name: 'main' }">Home</router-link>
              </li>
              <li class="nav-item">
                <router-link class="nav-link" :to="{ name: 'search' }">Search</router-link>
              </li>
              <li class="nav-item">
                <div v-if="!$root.store.username" class="text-end me-3">
                  <router-link class="nav-link" :to="{ name: 'register' }">Register</router-link>
                </div>
              </li>
              <li class="nav-item">
                <div v-if="!$root.store.username" class="text-end me-3">
                  <router-link class="nav-link" :to="{ name: 'login' }">Login</router-link>
                </div>
              </li>
              <li class="nav-item">
                <div v-if="$root.store.username" class="text-end me-3">
                  <button class="btn btn-link" @click="Logout">Logout</button>
                </div>
              </li>
              <!-- <li class="nav-item"> -->
                <!-- <div v-if="$root.store.username" class="text-end me-3">
                  <router-link class="nav-link" :to="{ name: 'create' }">Create Recipe</router-link> 
                </div> -->
              <!-- </li> -->
              <li class="nav-item">
                  <router-link class="nav-link" :to="{ name: 'about' }">About</router-link>
              </li>
              <li v-if="$root.store.username" class="nav-item dropdown" ref="dropdown">
                <a class="nav-link dropdown-toggle" href="#" id="privateAreaDropdown" role="button" :aria-expanded="isDropdownOpen.toString()" @click="toggleDropdown">
                  Private Area
                </a>
                <ul class="nav-link dropdown-menu" aria-labelledby="privateAreaDropdown" v-if="isDropdownOpen">
                  <li><router-link class="nav-link dropdown-item" :to="{ name: 'favorites' }">My Favorites</router-link></li>
                  <li><router-link class="nav-link dropdown-item" :to="{ name: 'MyRecipesPage' }">My Recipes</router-link></li>
                  <li><router-link class="nav-link dropdown-item" :to="{ name: 'familyRecipes' }">My Family Recipes</router-link></li>
                </ul>
              </li>
            </ul>
            <div v-if="$root.store.username">
              <b-button id="show-btn" @click="openCreateRecipe">Create Recipe</b-button>
              <b-modal ref="my-modal" hide-footer title="Using Component Methods">
                <div class="d-block text-center">
                  <!-- <h3>Hello From My Modal!</h3> -->
                </div>
              </b-modal>
            </div>

            <div class="d-flex justify-content-end align-items-center">
              <div v-if="!$root.store.username" class="displayUser text-end me-3">Hello Guest</div>
              <div v-else class="displayUser text-end me-3">{{ $root.store.username }}</div>
            </div> 
          </div>
        </div>
      </nav>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {   
  name: "App",
  data() {
    return {
      modalVisible: true,
      isDropdownOpen: false,
      create: this.$router.push({ name: 'create' }),
    };
  },
  mounted() {
    document.addEventListener("click", this.handleOutsideClick);
  },
  beforeUnmount() {
    document.removeEventListener("click", this.handleOutsideClick);
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

    toggleDropdown() {
      this.isDropdownOpen = !this.isDropdownOpen;
    },
    handleOutsideClick(event) {
      const dropdownElement = this.$refs.dropdown;
      if (!dropdownElement.contains(event.target)) {
        this.isDropdownOpen = false;
      }
    },
    openCreateRecipe() {
      const newWindow = window.open(this.$router.push({ name: 'create' }), "_blank", "width=800,height=600");
      this.$router.push({ name: 'main'})
      if (newWindow) {
        newWindow.onload = () => {
          newWindow.location.href = this.$router.resolve({ name: 'create' }).href;
        };
      } else {
        console.error("Failed to open a new window.");
      }
    },
    closeModal() {
      this.modalVisible = false;
    },
    showModal() {
        this.$refs['my-modal'].show()
      },
      hideModal() {
        this.$refs['my-modal'].hide()
      }
  }
};
</script>
<!-- // this.$router.
// if (newWindow) {
//   newWindow.onload = () => {
//     const newRouter = newWindow.VueRouterInstance; // Assuming you pass the Vue Router instance to the new window
    
//     // Use newRouter to navigate to a specific route in the new window
//     // newRouter.push({ name: 'create' });
//   };
// } else {
//   console.error("Failed to open a new window.");
// } -->
<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
}


#nav {
  padding: 30px;
    letter-spacing: 2px;
    color: white;
    font-size: 30px;
    font-weight: 50;
    border: 2px solid #ccd5d9;
    background-color:rgb(112, 147, 216);
    padding: 10px 10px;
    cursor: pointer;
    border-radius: 10px;
    animation: fadeIn 1s ease-in forwards;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color:rgb(112, 185, 216);
}


.displayUser {
    color: rgb(112, 143, 216);
    margin-left: auto;
    width: 10%;
    padding: 10px;
    background-color: #f8f9fa;
    text-align: right;
  }
</style>
