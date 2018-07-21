<template>
  <div id="app">
    <nav-component/>
    <b-container>
      <b-img center rounded="circle" :src="require('./assets/logo-girl.jpg')" fluid alt="Sorry, mama..." />
    </b-container>
    <form-component @responseToParent="onResponseRecieved"/>
    <b-container v-if="checkResponseEmptyness" fluid>
      <pick-component v-for="title in titles.result" :key="title.mal_id" :title="title"></pick-component>
    </b-container>
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue'
import NavComponent from './components/NavComponent.vue'
import PickComponent from './components/PickComponent.vue'

export default {
  name: 'app',

  data() {
    return{
      titles: {},
    }
  },

  components: {
    FormComponent,
    NavComponent,
    PickComponent,
  },

  methods: {
    onResponseRecieved (response){
      this.titles = response;
    }
  },

  computed: {
    checkResponseEmptyness(){
      return Object.keys(this.titles).length
    }
  }
}
</script>

<style lang="scss">
  #app{
    margin-bottom: 40px;
  }
</style>
