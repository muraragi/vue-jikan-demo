<template>
  <div id="app">
    <nav-component/>

    <b-container>
      <b-img center rounded="circle" :src="require('./assets/logo-girl.jpg')" fluid alt="Sorry, mama..." />
    </b-container>

    <hr>

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
        <b-container v-if="responseEmptyness">
          <h2 class="pick-header">Pick the correct one...</h2>
          <b-row v-for="titles in groupedTitles">
            <pick-component v-for="title in titles" :key="title.mal_id" :title="title" @passTimeWasted="receiveTimeWasted"></pick-component>
          </b-row>
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

</style>
