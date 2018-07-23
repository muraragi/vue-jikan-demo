<template>
    <div class="time-wasted-box">
        <h1>You have wasted {{ timeWasted }} minutes</h1>
    </div>
</template>

<script>
export default {
    name: "TimeWastedComponent",
    props: ['timeWasted'],
}
</script>

<style lang="scss" scoped>
    .time-wasted-box {
        display: flex;
        justify-content: center;
    }
</style>
