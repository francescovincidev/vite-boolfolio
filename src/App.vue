<script>
import axios from 'axios';

export default {
    data() {
        return {
            projects: []
        }

    },
    mounted() {
        this.getProjects();
    },
    methods: {
        getProjects() {
            axios.get('http://127.0.0.1:8000/api/projects').then(resp => {
                this.projects = resp.data.results;
            })
        }
    }

}

</script>

<template></template>

<style lang="scss"></style>
