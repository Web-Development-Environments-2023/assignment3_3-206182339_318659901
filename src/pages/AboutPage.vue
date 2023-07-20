<template>
  <div>
    <b-carousel class="carous"
      id="carousel-1"
      v-model="slide"
      interval="20000"
      controls
      indicators
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
      no-animation

    >

    <!-- /../assets/background-1.png -->
      <!-- Text slides with image -->
    
      <!-- Slides with custom text -->
      <b-carousel-slide img-src="https://img.freepik.com/free-photo/tomatoes-tomatoes-lemon-leaves-garlic-bottle-oil-tree-branches_140725-74118.jpg?w=996&t=st=1689774147~exp=1689774747~hmac=592f66be660be6a1debd9aeb4eb8da30e7718ddd2e4ba09aa865d81e8c6b2d1e">
        <h1 class="carousel-slide-title">Welcome to the Foodies!</h1>
        <p class="carousel-slide-text">
         Here you can find many recipes, create your own recipes, and see your traditional family recipes! <br>
        Have a recipe you like? Add to favorites! <br>
      Want to find something specific? Go to search recipe and look for specific recipe, from different cuisines, alergies and diets! <br>
    Hope you have fun! <br>
  Michal & Sean.   </p>
      <br>
   
      <br>
      </b-carousel-slide>
      <b-carousel-slide
       class="slide"
      caption="About"
      caption-tag="cap"
     
      img-src="https://media.istockphoto.com/id/1219874371/vector/abstract-hi-tech-technology-background.jpg?s=612x612&w=0&k=20&c=rRGZyjWl9-H-MdLRQogMQ0bWUCzpOo2Qa-u1LuQbV6U="
      >
          <div class="slide-content">
              <!-- <div class="links-container">
              </div> -->
              <div class="text-content">
                  <h1>Authors: Michal Alhindi & Sean Hacmon</h1>

                  <p>
                      <b-list-group-item><a class="links" href="https://github.com/MichalAlhindi" target=”_blank”>Michal's git</a></b-list-group-item>
                  </p>
                  <br>
                  
                  <p>
                      <b-list-group-item><a class="links" href="https://github.com/SeanHacmon" target=”_blank”>Sean's git</a></b-list-group-item>
                  </p>
                  <br>
                  
                  <p>
                      <b-list-group-item><a class="links" href="https://github.com/SeanHacmon/LooneyTunesGame" target=”_blank”>Shooting Tunes Game</a></b-list-group-item>
                  </p>
                  <br>
                  
                  <p>
                      <b-list-group-item><a class="links" href="https://github.com/SeanHacmon/SISE-Project-API-BackEnd" target=”_blank”>API & Server Project (3.2)</a></b-list-group-item>
                  </p>
                  <br>
                 
                  <p>
                       2 Software & Information System Engineers 3rd year students.
                  </p>
                 
                     <h1 class="michal"> Michal Responsibilty : </h1>
                  
                  <p>
                          Implementation of the pages - each page with he's unique Implementation.<br>
                          code Design - how the client will experience the UI.
                  </p>
              
                    <h1 class="sean">Sean Responsibilty :</h1> 
             
                  <p>
                          fixing bugs - issue small errors.<br>
                          code Structure - what components to create and who connects with who.
                  </p>
                 <br>
                 
              </div>
          </div>
      </b-carousel-slide>
    </b-carousel>

  </div>
</template>

<script>
  // export default {
  //   data() {
  //     return {
  //       slide: 0,
  //       sliding: null
  //     }
  //   },
  //   methods: {
  //     onSlideStart(slide) {
  //       this.sliding = true
  //     },
  //     onSlideEnd(slide) {
  //       this.sliding = false
  //     }
  //   }
  // }
</script>
<style>

.carous .carousel-control-prev,
.carous .carousel-control-next {
  width: 10%;
}

/* Customize carousel indicators */
.carous .carousel-indicators {
  bottom: 20px;
}

.carous .carousel-indicators li {
  background-color: #000;
  border-color: transparent;
  opacity: 0.5;
}

.carous .carousel-indicators .active {
  background-color: #000;
  opacity: 1;
}
.carousel-slide-title {
font-family: "Papyrus", sans-serif;
font-size: 35px; /* Adjust the font size as needed */
color: #336699; /* Your desired text color */
text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}
.carousel-slide-text {
font-family: "Papyrus", sans-serif;
font-size: 27px; /* Adjust the font size as needed */
color: #336699; 
text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);/* Your desired text color */
}
/* Customize slide content */
.slide-content {
  background-color: rgba(0, 0, 0, 0.7);
  color: #fff;
  padding: 20px;
  text-align: center;
}

.slide-content h1 {
  font-size: 24px;
  margin-bottom: 10px;
}

.slide-content p {
  font-size: 16px;
  line-height: 1.5;
  margin-bottom: 10px;
}

/* Customize links */
.links {
  color: #407dbf;
  text-decoration: none;
}

.links:hover {
  text-decoration: underline;
}

/* Customize text alignment */
.sean {
  text-align: center;
}

.michal {
  text-align: center;
}
cap{
  font-size: 56px;
  font-family: Monaco, monospace;
}
</style>