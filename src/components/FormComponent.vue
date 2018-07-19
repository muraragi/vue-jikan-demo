<template>
  <b-container class="wrapper">
    <b-form @submit="onSubmit" @reset="onReset">
      <b-form-group id="mainFormGroup"
                    label="Anime title:"
                    label-for="title"
                    description="We'll never share your precious secrets with your parents.">
        <b-form-input id="title"
                      type="text"
                      v-model="form.title"
                      required
                      placeholder="Enter the title...">
        </b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary" class="left">Seek your destiny</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </b-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'FormComponent',
  data () {
    return {
      form: {
        title: ''
      },
    }
  },
  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      // alert(JSON.stringify(this.form));
      axios.get('https://api.jikan.moe/search/anime' + this.form.title)
        .then(respone => {
          console.log(respone)
        })
        .catch(error => {
          console.log(error)
        })
    },
    onReset (evt) {
      evt.preventDefault()
      /* Reset our form values */
      this.form.email = ''
      this.form.name = ''
      this.form.food = null
      this.form.checked = []
      /* Trick to reset/clear native browser form validation state */
      this.show = false
      this.$nextTick(() => { this.show = true })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .wrapper{
    border: 1px solid #c3c3c3;
    padding: 10px;
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  }

  .left{
    margin-right: 10px
  }
</style>
