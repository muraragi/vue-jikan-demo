<template>
  <div id="app">
    <nav-component/>

    <b-container class="image-wrapper">
      <b-img center rounded :src="require('./assets/logo-girl.jpg')" fluid width="700px" alt="Sorry, mama..."/>
    </b-container>


    <transition name="fade">
      <b-container v-if="timeWasted">
        <time-wasted-component :timeWasted="timeWasted"></time-wasted-component>
        <div class="button-container">
          <b-button variant="success" @click="reset">Check another title...</b-button>
        </div>
      </b-container>
    </transition>

    <div v-if="!timeWasted">
      <transition name="fade">
        <div v-if="!responseEmptyness">
          <form-component @responseToParent="onResponseRecieved"/>
        </div>
      </transition>

      <transition name="fade">
        <b-container v-if="responseEmptyness" class="pick-wrapper">
          <div class="pick-header">
            <h2>Pick the correct one...</h2>
          </div>
          <b-row v-for="(titles, index) in groupedTitles" :key="`titles-${index}`">
            <pick-component v-for="title in titles" :key="title.mal_id" :title="title" @passTimeWasted="receiveTimeWasted"></pick-component>
          </b-row>
          <div class="pick-footer">
            <hr>
            <b-button variant="warning" @click="reset">Return to search</b-button>
          </div>
        </b-container>
      </transition>
    </div>
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue'
import NavComponent from './components/NavComponent.vue'
import PickComponent from './components/PickComponent.vue'
import TimeWastedComponent from './components/TimeWastedComponent.vue'

export default {
  name: 'app',

  data () {
    return {
      titles: {},
      timeWasted: 0
    }
  },

  components: {
    FormComponent,
    NavComponent,
    PickComponent,
    TimeWastedComponent
  },

  methods: {
    onResponseRecieved (response) {
      this.titles = response
    },

    receiveTimeWasted (timeWasted) {
      console.log(timeWasted)
      this.timeWasted = timeWasted
    },

    reset () {
      this.titles = {}
      this.timeWasted = 0
    },

    chunkArray(myArray, chunk_size){
      let index = 0;
      let arrayLength = myArray.length;
      let tempArray = [];
      
      for (index = 0; index < arrayLength; index += chunk_size) {
          let myChunk = myArray.slice(index, index+chunk_size);
          // Do something if you want with the group
          tempArray.push(myChunk);
      }

    return tempArray;
}
  },

  computed: {
    responseEmptyness () {
      return Object.keys(this.titles).length
    },
    groupedTitles() {
      return this.chunkArray(this.titles, 3)
      // returns a nested array: 
      // [[article, article, article], [article, article, article], ...]
    }
  }
}
</script>

<style lang="scss">
  #app{
    margin-bottom: 40px;
  }

  hr{
    width: 50%;
    border: 0;
    height: 1px;
    background: #333;
    background-image: linear-gradient(to right, #ccc, #333, #ccc);
  }

  .button-container{
    text-align: center;
    margin-top: 10px;
  }

  .pick-header{
    text-align: center;
  }

  .pick-footer{
    text-align: center;
  }

  .image-wrapper{
    margin-bottom: 20px
  }

  .pick-wrapper{
    border: 1px solid rgba(0,0,0,0.22);
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    padding: 20px;
  }

</style>
