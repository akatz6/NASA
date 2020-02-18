<template>
<div class="">
  <div id="moreImages">
    <button v-if="counter > 1" type="button" class="btn btn-lg btn-primary m-4" @click="prevImages">
      Previous
    </button>
    <button v-if="counter < 40" type="button" class="btn btn-lg btn-primary m-4" @click="nextImages">
      Next
    </button>
  </div>
  <div id="roverImagesPage">
    <div v-for="rover in roverJsonArray" class="">
      <img :src="rover['img_src']" :alt="rover['rover']['name']">
      <br>
      <p>
        Taken using {{rover['camera']['full_name']}}
        by the {{rover['rover']['name']}}
      </p>
      <br><br><br>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';
export default {

  data() {
    return {
      roverJsonArray: [],
      counter: 1,
      apiStringFirstHalf: "https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&page=",
      apiStringSecondHalf: "&api_key=tCa2D1VdFJjVRGYhYfXxC4HjPUsRHU8CGGNQovpe"
    }
  },
  created() {
    this.callApi();
  },
  methods: {
    prevImages: function() {
      this.counter--;
      this.callApi();
    },
    nextImages: function() {
      this.counter++;
      this.callApi();
    },
    callApi: function() {
      axios.get(`${this.apiStringFirstHalf}${this.counter}${this.apiStringSecondHalf}`)
        .then(res => {
          this.roverJsonArray = res.data['photos'];
          this.roverJsonArray = this.roverJsonArray.splice(0, 20);
          console.log(this.roverJsonArray)
        })
        .catch(error => console.log(error))
    }
  }
}
</script>

<style scoped lang="scss">
#moreImages {
    margin: 3%;
    display: flex;
    justify-content: flex-end;
}
#roverImagesPage {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    grid-gap: 1%;
    margin-left: 5%;
    margin-right: 5%;
    img {
        width: 200px;
        height: 200px;
    }
}
</style>
