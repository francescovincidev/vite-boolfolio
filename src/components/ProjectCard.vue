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
            <p class="text-primary">
            <div>

                <span v-if="project.type">{{ project.type.name }}</span>
                <span v-else>Nessun tipo</span>
            </div>
            <div>

                <template v-if="project.technologys.length >= 1"><span v-for="(technology, index) in project.technologys"
                        :key="index">{{
                            technology.name
                        }}<span v-if="index !== project.technologys.length - 1">, </span> </span></template>
                <span v-else>Nessuna tecnologia</span>
            </div>
            </p>
        </div>
    </div>
</template>

<style lang="scss" scoped></style>