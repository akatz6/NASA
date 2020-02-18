<template>
  <div id="currentLocationDiv">
    <img :src="location['url']"
    id="currentLocationImage" class="">
    <p id="currentLocationExplanation">A NASA image of
      latitude {{latitude}} and longitude {{longitude}}
      This is your current location
  </p>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data(){
    return{
      latitude: "",
      longitude: "",
      location: "",
    }
  },
  created() {
    navigator.geolocation.getCurrentPosition(this.getLatLon);

  },
  methods:{
    getLatLon: function (position) {
   this.latitude = position.coords.latitude;
   this.longitude = position.coords.longitude;
   this.latitude = this.latitude.toFixed(3)
   this.longitude = this.longitude.toFixed(3)
   axios.get(`https://api.nasa.gov/planetary/earth/imagery/?lon=${this.longitude}&lat=${this.latitude}&date=2014-02-01&cloud_score=True&api_key=tCa2D1VdFJjVRGYhYfXxC4HjPUsRHU8CGGNQovpe`)
     .then(res => {
       this.location = res.data;
     })
     .catch(error => console.log(error))
}
  }
}
</script>

<style lang="scss" scoped>

#currentLocationDiv{
  padding-bottom: 100px;

  #currentLocationImage{
    width: 20%
  }

  #currentLocationExplanation{
    margin: 0 auto;
    width: 20%;
    margin-top: 2%;
  }
}


</style>
