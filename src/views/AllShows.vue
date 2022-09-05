<template>
  <v-container >

    <v-row justify="center">

      <v-col cols="12">
        <div class="showsByPage">Page {{pageNumber}} of 500 </div>
        <br/>
        <v-pagination
          :total-visible="9"
          v-model="pageNumber"
          :length="500"
          circle
        ></v-pagination>
      </v-col>

      <v-container v-if="!resetIt" cols="12" md="3">
        <v-row>
          <v-col  v-for="index in 32" :key="index" cols="12" md="3">
            <PagedShows  :key="NaN" :index="index+((pageNumber-1)*32)"/>
          </v-col>
        </v-row>
        
      </v-container>
      <br/>
        <v-pagination
          :total-visible="9"
          v-model="pageNumber"
          :length="500"
          circle
        ></v-pagination>
    </v-row>
    <br /><br />

    <div>
      <button @click="topFunction()" class="myBtn">Go to Top</button>
    </div>
    

  </v-container>
  
</template>



<script>
import PagedShows from '../components/PagedShows.vue';
export default {
  components: { PagedShows},
  name: "AllShows",

  data() {
    return {
      pageNumber: 1,
      resetIt:false,
    };
  },

  methods:{
    topFunction(){
      window.scrollTo({
          top: 0,
          behavior: "smooth"
        });
    },
  },

  watch: {
    resetIt: function () {
      if(this.resetIt){
        this.pageNumber++;
        window.scrollTo({
          top: 0,
          behavior: "smooth"
        });
        this.resetIt=false;
      }
      
    },
  },


};
</script>

<style lang="scss" scoped>

@font-face {
  font-family: "Stargaze";
  src: local("Stargaze"),
   url("../fonts/Stargaze Stencil.otf") format("truetype");
}

.showsByPage {
  font-family:Stargaze;
  text-align: center;
  text-transform: uppercase;
  font-size: 50px;
  color: white;
  background: rgba(200, 200, 200, 0.7);
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