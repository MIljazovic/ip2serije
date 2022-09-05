<template>
  <v-row v-if="showFlag" :key="NaN">
    <v-col>

      <div class="image">
          <a  :href="show.url" target="_blank">
            <img :src="show.image.medium" />
          </a>
      </div>
     
      <v-card class="mainCard" color="#5f5f5f" height="auto" width="252px">
        <div class="card" ><span>{{ show.name }}</span></div>
        <div class="cardText">
          <b>Language:</b> {{ show.language }} <br />
          <b>Type:</b> {{ show.type }} <br />
          <b>Aired from:</b> {{ show.premiered }} <b>to</b> {{ show.ended }} <br />
          <b>Status:</b> {{ show.status }} <br />
          <b>Score:</b> {{ show.rating.average }}
        </div>
        <div class="dialog">
          <v-dialog v-model="favourite" width="500">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="amber darken-3" dark v-bind="attrs" v-on="on">
                <span>Favourite</span>
              </v-btn>
            </template>

            <v-card>
              <v-card-title class="text-h5 grey lighten-2">
                Favourite?
              </v-card-title>

              <v-card-text>
                Are you sure you want to add this show to your favourites list?
              </v-card-text>

              <v-divider></v-divider>

              <v-card-actions>
                <v-btn
                  color="green"
                  text
                  @click="
                    favourite = false;
                    successAlert = true;
                  "
                >
                  Yes, I do.
                </v-btn>
                <v-spacer></v-spacer>
                <v-btn
                  color="red"
                  text
                  @click="
                    favourite = false;
                    failedAlert = true;
                  "
                >
                  No, I don't.
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </div>
      </v-card>

      <v-alert class="alert"   type="success"  :value="successAlert">
        Successfully added to favourites!</v-alert
      >

      <v-alert class="alert"  type="error" color="black" dismissible :value="failedAlert">
        Seems like you've changed your mind!</v-alert
      >

    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      favourite: false,
      successAlert: false,
      failedAlert: false,
      show:[],
      showFlag: true,
    };
  },
  props: ["index"],




  created() {
    this.getAllShows();
  },


  methods:{
    //TEST ZA API
    getAllShows(){
        let api = "https://api.tvmaze.com/shows/" + this.index;
        this.axios.get(api).then((response) => { 
          this.show = response.data;
        }).catch((error) => {
          if(error.response || error.request){this.index=Math.floor(Math.random() * 10000);}
        });
    },


  },

  watch:{
    index: function(){
      this.getAllShows();
    },
    successAlert: function(){
      setTimeout(()=>{
      this.successAlert=false;
    },3000)
    },
    failedAlert: function(){
      setTimeout(()=>{
      this.failedAlert=false;
    },3000)
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



.mainCard{
  margin-left: auto;
  margin-right: auto;
}
.card {
  overflow: auto;
  max-height: 80px;
  text-align: center;
  line-height: 80px;
  font-family:Stargaze;
  font-size:25px;
  font-weight: bold;
}

.card span{
  display: inline-block;
  vertical-align: middle;
  line-height: normal;
}


.cardText {
  min-height: 200px;
  background-color: grey;
  padding-left:10px;
  padding-bottom: 10px;
  font-size: 20px;
}

.dialog {
  padding: 10px;
  text-align: center;
}

.image {
  
  scale: 1.2;
  text-align: center;
  margin-top:50px;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 20px;
}
.alert{
  position:absolute;
}

</style>