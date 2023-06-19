<template>
    <div>
      <b-carousel class="carous"
        id="carousel-1"
        v-model="slide"
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
        <b-carousel-slide
         class="slide"
        caption="About"
        caption-tag="cap"
        text="Authors: Michal Alhindi & Sean Hacmon"
        img-src="https://img.freepik.com/free-vector/matrix-style-binary-code-digital-falling-numbers-blue-background_1017-37387.jpg?size=626&ext=jpg&ga=GA1.2.6476563.1687103082&semt=ais"
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
                    <br>
                    <p>
                        <b-list-group-item><a class="links" href="https://github.com/SeanHacmon" target=”_blank”>Sean's git</a></b-list-group-item>
                    </p>
                    <br>
                    <br>
                    <p>
                        <b-list-group-item><a class="links" href="https://github.com/SeanHacmon/LooneyTunesGame" target=”_blank”>Shooting Tunes Game</a></b-list-group-item>
                    </p>
                    <br>
                    <br>
                    <p>
                        <b-list-group-item><a class="links" href="https://github.com/SeanHacmon/SISE-Project-API-BackEnd" target=”_blank”>API & Server Project (3.2)</a></b-list-group-item>
                    </p>
                    <br>
                    <br>
                    <p>
                         2 Software & Information System Engineers 3rd year students.
                    </p>
                    <p class="michal">
                        &nbsp; &nbsp; &nbsp; &nbsp; Michal Responsibilty :
                    </p>
                    <p>
                            Implementation of the pages - each page with he's unique Implementation.<br>
                            code Design - how the client will experience the UI.
                    </p>
                    <p class="sean">
                        &nbsp; &nbsp; &nbsp; &nbsp; Sean Responsibilty :
                    </p>
                    <p>
                            fixing bugs - issue small errors.<br>
                            code Structure - what components to create and who connects with who.
                    </p>
                   <br>
                   <br>
                   <br>
                </div>
            </div>
        </b-carousel-slide>
        <!-- Slides with custom text -->
        <b-carousel-slide img-src="https://www.astera.com/wp-content/uploads/2020/01/rest.png">
          <h1>Summary</h1>
          <p>
            We have used our server component & our API (from 3.2).
          </p>
          <p>
            We have used spoonacular as our main data base
          </p>
          <p>
            We connected between the requests we get from the client via our website with the spoonacular data.
          </p>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
        <br>
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
    color: #fff;
    text-decoration: none;
  }

  .links:hover {
    text-decoration: underline;
  }

  /* Customize text alignment */
  .sean {
    text-align: left;
  }

  .michal {
    text-align: left;
  }
  cap{
    font-size: 56px;
    font-family: Monaco, monospace;
  }
</style>