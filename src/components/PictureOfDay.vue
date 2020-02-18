<template>
<div>
  <h2>{{pictureOfDayJSON['title']}}</h2>
  <img :src="pictureOfDayJSON['hdurl']" :alt="pictureOfDayJSON['title']" id="nasaImageOfDay" class="">
  <p id="nasaImageExplanation">{{pictureOfDayJSON['explanation']}}</p>
</div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      pictureOfDayJSON: ""
    }
  },
  created() {
    axios.get("https://api.nasa.gov/planetary/apod?api_key=tCa2D1VdFJjVRGYhYfXxC4HjPUsRHU8CGGNQovpe")
      .then(res => {
        this.pictureOfDayJSON = res.data;
        console.log(this.pictureOfDayJSON)
      })
      .catch(error => console.log(error))
  }
}
</script>

<style lang="css" scoped>
  #nasaImageOfDay{
    width: 65%;
    margin: 3%;
  }

  #nasaImageExplanation{
    width: 65%;
    margin: 0 auto;
  }
</style>
