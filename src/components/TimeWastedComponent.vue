<template>
    <div class="time-wasted-box">
        <h1>You have wasted {{ computedTimeWasted }}</h1>
    </div>
</template>

<script>
export default {
  name: 'TimeWastedComponent',
  props: ['timeWasted'],
  computed: {
      computedTimeWasted(){
        let type = this.timeWasted.type
        let timeWastedString = ""
        if(this.timeWasted.type === "Movie"){
            let filteredDurationString = this.timeWasted.duration.replace(/\D+/g, "")
            let minutes = filteredDurationString.split("").splice(1).join("")
            let hours = filteredDurationString.split("").splice(0, 1).join("")
            timeWastedString = `${hours} hours and ${minutes} minutes`
        }
        else{
            let episodes = this.timeWasted.episodes
            let avgDuration = parseInt(this.timeWasted.duration)
            let minutes = (episodes * avgDuration)%60
            let hours = (episodes * avgDuration - minutes)/60
            timeWastedString = `${hours} hours and ${minutes} minutes`
        }

        return timeWastedString
      }
  }
}
</script>

<style lang="scss" scoped>
    .time-wasted-box {
        display: flex;
        justify-content: center;
    }
</style>
