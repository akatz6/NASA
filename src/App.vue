<template>
<div id="app">
  <ul class="nav nav-tabs">
    <li class="nav-item">
      <a class="nav-link" @click="selectedComponent = 'appMars'">Mars Rover Photos</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" @click="selectedComponent = 'appPic'">Astronomy Picture Of Day</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" @click="selectedComponent = 'appLocation'">Current Location</a>
    </li>
  </ul>
  <component :is="selectedComponent" id="dynamicComponent">
  </component>
</div>
</template>

<script>
import Mars from './components/MarsRoverPhotos.vue';
import Location from './components/CurrentLocation.vue';
import Pic from './components/PictureOfDay.vue';
import axios from 'axios';

export default {
  data() {
    return {
      selectedComponent: 'appPic',
    }
  },
  components: {
    appMars: Mars,
    appPic: Pic,
    appLocation: Location,
  }
}
</script>

<style lang="scss">
body {
    background-image: linear-gradient(to bottom right, #F0F8FF, #191970);
}
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;

    #dynamicComponent {
        padding-top: 30px;
    }

    p {
        text-align: left;
    }
}
</style>
