<template>
  <v-sheet height="512px" tile>
    <v-row v-if="showFlag" :key="NaN" class="mb-6">
      
      <v-col xl="10" lg="8" md="8" sm="7" xs="12" style="text-align:start;">
        <div class="card" ><span>{{ show.name }}</span></div>
        <div class="cardText">
          <b>Language:</b> {{ show.language }} <br />
          <b>Type:</b> {{ show.type }} <br />
          <b>Aired from:</b> {{ show.premiered }} <b>to</b> {{ show.ended }} <br />
          <b>Status:</b> {{ show.status }} <br />
          <b>Score:</b> {{ show.rating.average }}
          <br />
          <b>Summary:</b> 
          <div>
            {{show.summary}}
          </div>
          <br/>
          <br/>
          <br/>
        </div>
      </v-col>

      <v-col xl="2" lg="4" md="4" sm="5" xs="12" style="text-align:end;">
        <div class="image">
          <a  :href="show.url" target="_blank">
            <img :src="show.image.original" contain height="500px"/>
          </a>
      </div>
      </v-col>

    </v-row>            
  </v-sheet>

</template>

<script>
export default {
  data() {
    return {
      show:[],
      showFlag: true,
    };
  },
  props: ["index"],




  created() {
    this.getAllShows();
  },


  methods: {
    //TEST ZA API
    getAllShows(){
        let api = "https://api.tvmaze.com/shows/" + this.index;
        this.axios.get(api).then((response) => { 
          this.show = response.data;
          this.show.summary = this.show.summary.replace(/<\/?[^>]+(>|$)/g, "")
        }).catch((error) => {
          if(error.response || error.request){this.index=Math.floor(Math.random() * 10000);}
        });
    },


  },

  watch:{
    index: function(){
      this.getAllShows();
    },
  }
};

</script>






<style lang="scss" scoped>

@font-face {
  font-family: "Stargaze";
  src: local("Stargaze"),
   url("../fonts/Stargaze Stencil.otf") format("truetype");
}



.mainCard{
  margin-left: auto;
  margin-right: auto;
}
.card {
  width: auto;
  overflow: auto;
  min-height: 110px;
  text-align: center;
  line-height: 80px;
  font-family:Stargaze;
  font-size:40px;
  font-weight: bold;
}



.cardText {
  width: auto;
  overflow: auto;
  max-height:320px;
  padding-left:20px;
  font-size: 20px;
}

</style>