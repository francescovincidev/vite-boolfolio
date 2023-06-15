<script>
export default {
    name: 'ProjectCard',
    data() {
        return {
            technologyArray: []
        }

    },
    props: {
        project: Object
    },
    computed: {

    }

}
</script>

<template>
    <div class="card h-100">
        <div class="card-body">
            <h5>{{ project.title }}</h5>
            <p>{{ project.content }}</p>
            <p class="text-primary">
            <div>

                <span v-if="project.type">Tipo: {{ project.type.name }}</span>
                <span v-else>Nessun tipo</span>
            </div>
            <div>

                <template v-if="project.technologys.length">Tecnologie: <span
                        v-for="(technology, index) in project.technologys" :key="index">{{
                            technology.name
                        }}{{ index === project.technologys.length - 1 ? '' : ', ' }} </span></template>
                <span v-else>Nessuna tecnologia</span>
            </div>
            </p>
            <router-link :to="{ name: 'single-projects', params: { slug: project.slug } }"
                class="btn btn-primary">Visualizza dettagli</router-link>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>