<template>
  <div id="app">
    <nav-component/>
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
