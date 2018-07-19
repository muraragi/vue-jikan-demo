<template>
  <div id="app">
    <nav-component/>
    <b-container>
      <b-img center rounded="circle" :src="require('./assets/logo-girl.jpg')" fluid alt="Sorry, mama..." />
    </b-container>
    <form-component/>
  </div>
</template>

<script>
import FormComponent from './components/FormComponent.vue'
import NavComponent from './components/NavComponent.vue'

export default {
  name: 'app',
  components: {
    FormComponent,
    NavComponent
  }
}
</script>

<style lang="scss">

</style>
