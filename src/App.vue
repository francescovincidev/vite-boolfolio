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
                this.projects = resp.data.results.data;
            });
        }
    },
    components:
        { ProjectCard }

}

</script>

<template>
    <div class="container">
        <h1>Progetti</h1>
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
