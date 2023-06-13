<script>
import axios from 'axios';
import ProjectCard from './components/ProjectCard.vue';

export default {

    data() {
        return {
            projects: []
        };

    },
    mounted() {
        this.getProjects();
    },
    methods: {
        getProjects() {
            axios.get('http://127.0.0.1:8000/api/projects').then(resp => {
                this.projects = resp.data.results;
            });
        }
    },
    components:
        { ProjectCard }

}

</script>

<template>
    <div class="container">
        <div class="row row-cols-3">
            <div class="col" v-for="project in projects" :key="project.id">

                <ProjectCard :project="project" />

            </div>
        </div>
    </div>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>
