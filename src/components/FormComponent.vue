<template>
  <div>

    <div v-if="loading">
        <spinner></spinner>
    </div>

    <b-container class="wrapper" v-else>
      <div>
        <div class="preview">
          <h1>Lets embarrass yourselfs</h1>
        </div>

        <hr>

        <b-form @submit="onSubmit">
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
          <div class="buttons">
            <b-button type="submit" variant="primary" class="left">Seek your destiny</b-button>
          </div>
        </b-form>
      </div>
    </b-container>

  </div>
</template>

<script>
import axios from 'axios'
import Spinner from './Spinner.vue'

export default {
  name: 'FormComponent',
  data () {
    return {
      form: {
        title: ''
      },
      loading: false
    }
  },
  components: {
    Spinner
  },

  methods: {
    onSubmit (evt) {
      evt.preventDefault()
      this.loading = true
      axios.get('https://api.jikan.moe/search/anime/' + this.form.title)
        .then(response => {
          console.log(response.data)
          this.$emit('responseToParent', response.data.result.slice(0, 9))
          this.loading = false
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .wrapper{
    border: 1px solid #c3c3c3;
    padding: 20px;
    padding-bottom: 60px;
    margin-bottom: 40px;
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  }

  .left{
    margin-right: 10px
  }

  .preview{
    text-align: center;
  }

  hr{
    width: 50%;
    border: 0;
    height: 1px;
    background: #333;
    background-image: linear-gradient(to right, #ccc, #333, #ccc);
  }

  #mainFormGroup{
    width: 80%;
    margin: 0 auto;
    margin-bottom: 10px;
  }

  .buttons{
    width: 80%;
    margin: 0 auto;
  }
</style>
