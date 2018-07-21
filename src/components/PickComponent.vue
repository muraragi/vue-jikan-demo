<template>
    <b-container>
        <b-card border-variant="primary"
                :header="title.title"
                header-bg-variant="primary"
                header-text-variant="white"
                align="center">
        <p class="card-text">{{ title.description }}</p>
        </b-card>
    </b-container>
</template>

<script>
export default {
    name: 'PickComponent',
    props: ['title']
}
</script>

<style>

</style>
