<template>
    <b-col cols="12" lg="4" class="one-card">
        <b-img rounded="circle" width="120" thumbnail :src="title.image_url" alt="Thumbnail" class="title-picture"/>
        <b-button variant="danger" size="sm" class="choose-button" @click="getTimeWasted(title.mal_id)">
            {{ title.title }}
        </b-button>
    </b-col>
</template>

<script>
import axios from 'axios'

export default {
  name: 'PickComponent',
  props: ['title'],
  methods: {
    getTimeWasted (id) {
      axios.get('https://api.jikan.moe/anime/' + id)
        .then(response => {
          console.log(response.data)
          console.log(response.data.duration.replace(/\D+/g, ""))  

          this.$emit('passTimeWasted', response.data)
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<style lang="scss">
    .one-card{
        display: flex;
        margin-bottom: 20px;
        justify-content: center;
        flex-wrap: wrap;
    }

    .title-picture{
        margin-bottom: 5px;
    }

    .choose-button{
        width: 90%;
        overflow: hidden;
    }
</style>
