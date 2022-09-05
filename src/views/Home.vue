<template>

  <v-container >

    <v-row> 
      <v-col cols="12" style="margin:auto;">
        <div class="WelcomeText">Welcome to the Tv-Shows Database webpage</div>
      </v-col>
      <v-col cols="8" style="margin:auto;">
        <div class="AboutText1">
          On this Webpage you can look up information about various shows from all countries in the world. 
          <br/>
          By clicking on the expandable toolbar icon in the top left corner you can traverse through this webpage.
        </div>
      </v-col>
      <v-col cols="4" style="margin:auto;">
        <div class="AboutText2">It was created as a college project and uses 
          <a href="https://www.tvmaze.com/api" target="_blank">
            <img src="../assets/tvmaze.png" width="350px" style="margin-top:10px" />
          </a>
        </div>     
      </v-col>


      <v-col cols="12">
        <v-carousel v-model="currentIndex">
          <v-carousel-item v-for="show in shows" :key="show">
            <HomeShows :index="show" />
          </v-carousel-item>
        </v-carousel> 
      </v-col>


    </v-row>
  </v-container>
</template>

<script>
import HomeShows from '../components/HomeShows.vue';
export default {
  components: { HomeShows},
  name: "Home",

  data() {
    return {
      currentIndex:0,
      shows: [],
    };
  },

  created(){
    this.getShows();
  },

  methods: {
    getShows(){
      for (let index = 0; index < 10; index++) {
        this.shows[index]=Math.floor(Math.random() * 1000);
        
      }
    }
  }

};
</script>

<style lang="scss" scoped>

@font-face {
  font-family: "Stargaze";
  src: local("Stargaze"),
   url("../fonts/Stargaze Stencil.otf") format("truetype");
}
@font-face {
  font-family: "Blackthorn";
  src: local("Blackthorn"),
   url("../fonts/blackthorn.ttf") format("truetype");
}

.WelcomeText {
  padding: 10px 5px 10px 5px;
  text-align: center;
  font-family: Stargaze;
  font-size: 30px;
  color: white;
  background: rgba(200, 200, 200, 1);
  border-radius: 25px;
}

.AboutText1 {
  padding: 14px 5px 14px 5px;
  text-align: center;
  font-family: Blackthorn;
  font-size: 25px;
  color: white;
  background: rgba(200, 200, 200, 1);
  border-radius: 25px;
}
.AboutText2 {
  padding: 5px 5px 5px 5px;
  text-align: center;
  font-family: Blackthorn;
  font-size: 25px;
  color: white;
  background: rgba(200, 200, 200, 1);
  border-radius: 25px;
}

.hrefEle{
  text-decoration: none;
  color: white;
}

</style>