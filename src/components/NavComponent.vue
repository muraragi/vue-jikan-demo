<template>
    <b-navbar toggleable="md" type="dark" variant="dark" class="navbar">

        <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

        <b-navbar-brand href="#" class="brand">How much time have you wasted?</b-navbar-brand>

        <b-collapse is-nav id="nav_collapse">
            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
                <a href="https://github.com/muraragi/vue-jikan-demo">
                    <i class="fab fa-github fa-2x">
                    </i>
                </a>
            </b-navbar-nav>

        </b-collapse>
    </b-navbar>

</template>

<script>
export default {
  name: 'NavComponent'
}
</script>

<style lang="scss" scoped>
    .navbar{
        margin-bottom: 40px;
        box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
    }

    .brand{
        font-family: 'Chela One', cursive;
    }

    .fa-github{
        color: white;
    }
</style>
