<script>
export default {
    name: "NotFound",
    methods: {
        goBack() {
            console.log(this.$router);
            this.$router.back();
        }
    }
}
</script>

<template>
    <h2 class="text-center my-5">Pagina che stai cercando non esiste.</h2>
    <router-link :to="{ name: 'home' }" class="btn btn-success">Go home</router-link>
    <a @click.prevent="goBack" class="btn btn-warning" href="">Go back</a>
</template>

<style lang="scss" scoped></style>