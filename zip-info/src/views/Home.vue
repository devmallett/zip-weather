<template>
  <div class="ion-page">
   <ion-header>
      <ion-toolbar>
        <ion-title>ZipInfo</ion-title>
      </ion-toolbar>
    
   </ion-header>

   <ion-content class="ion-padding">
     <ZipSearch v-on:get-zip="getZipInfo"/>
     <ZipInfo  v-bind:info="info"/>
     <ClearInfo v-bind:info="info" v-on:clear-info="clearInfo"/>
   </ion-content>
  </div>
</template>

<script>
// @ is an alias to /src
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
import ClearInfo from "../components/ClearInfo";

export default {
  name: 'Home',
  components: {ZipSearch, ZipInfo, ClearInfo},
  data() {
    return{
      info: null

    }

  },
  methods: {
    async getZipInfo(zip){
      // console.log(zip + " get Zip Info ")
      const res = await fetch(`http://api.zippopotam.us/us/${zip}`);
      this.info = await res.json();

      // console.log(info)
      // Making sure not 404
      if(res.status == 404){
        this.showAlert();
      }
    },
    clearInfo(){
      this.info=null;
    },

    showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Not valid Zip",
                message: "Enter a valid zip code",
                buttons: ["OK"]
            })
            .then( a => a.present())
        }
  }
}
</script>
