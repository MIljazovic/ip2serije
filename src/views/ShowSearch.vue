<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="12">
        <div class="searchShow">Search for a show:</div>
      </v-col>

      <v-col cols="12">
        <v-text-field
          append-icon="mdi-magnify"
          dark
          filled
          label="3 letters minimum!"
          placeholder="Dar Mar, Full House, Family Matters etc."
          v-model="search"
          :loading="isLoading"
          @submit.prevent="search"
          clearable
          :rules="inputRules"
        ></v-text-field>
      </v-col>

    </v-row>
    <v-row v-if="!showFlag" :key="NaN">
      
      <v-col
        v-for="series in show"
        :key="series"
        cols="12"
      >
      <show-cards :index="series.show.id">

      </show-cards>
      </v-col>

    </v-row>

    <div>
      <button @click="topFunction()" class="myBtn">Go to Top</button>
    </div>

  </v-container>
</template>

<script>
import ShowCards from "../components/SearchShow.vue";

export default {
  components: { ShowCards },
  name: "ShowSearch",

  data() {
    return {
      show:[],
      showFlag: false,
      search: "",
    };
  },

  created() {
    this.getAllShows();
  },

  methods: {
 //TEST ZA API
 getAllShows(){
        let api = "https://api.tvmaze.com/search/shows?q=" + this.search;
        this.axios.get(api).then((response) => { 
          this.show = response.data;
          this.show.summary = this.show.summary.replace(/<\/?[^>]+(>|$)/g, "")
        }).catch((error) => {
          if(error.response || error.request){this.index=Math.floor(Math.random() * 10000);}
        });
      },
  topFunction(){
      window.scrollTo({
          top: 0,
          behavior: "smooth"
        });
    },
  },

  watch: {
    search: function () {
      this.getAllShows();
      this.showFlag=!this.showFlag;
      window.scrollTo(0, 0);
    },
    showFlag: function (){
      if(this.showFlag==true){
      this.showFlag=!this.showFlag;
    }
    }
    
  },
};
</script>

<style lang="scss" scoped>
.searchShow {
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bold;
  font-size: 40px;
  color: white;
  background: rgba(200, 200, 200, 0.9);
  border-radius: 25px;
}
.myBtn {
  position: fixed;
  bottom: 20px;
  right: 30px;
  z-index: 99; 
  border: none; 
  outline: auto;
  background-color: grey; 
  color: #3f3f3f; 
  cursor: pointer;
  padding: 15px; 
  border-radius: 10px;
  font-size: 20px; 
}

.myBtn:hover {
  scale:120%;
  background-color: #666;
}
</style>