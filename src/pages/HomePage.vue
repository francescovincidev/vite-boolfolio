<script>
export default {
    name: "HomePage"
}
</script>

<template>
    <div class="container">
        <h2>Benvenuto</h2>
        <router-link :to="{ name: 'projects' }">Visualizza i tuoi progetti</router-link>

    </div>
</template>

<style lang="scss" scoped></style>