<script>
import axios from 'axios';
import ProjectCard from './components/ProjectCard.vue';

export default {

    data() {
        return {
            projects: [],
            currentPage: 1,
            lastPage: null,
            totalProjects: 0,
        };

    },
    mounted() {
        this.getProjects();
    },
    methods: {
        getProjects(pageNumber = 1) {
            axios.get('http://127.0.0.1:8000/api/projects', {
                params: {
                    page: pageNumber
                }
            }).then(resp => {
                this.projects = resp.data.results.data;
                this.currentPage = resp.data.results.current_page;
                this.lastPage = resp.data.results.last_page;
                this.totalProjects = resp.data.results.total;
            });
        }
    },
    components:
        { ProjectCard }

}

</script>

<template>
    <div class="container">
        <h1 class="text-center mt-3 mb-4">Progetti</h1>
        <div class="row row-cols-4 g-3">
            <div class="col" v-for="project in projects" :key="project.id">

                <ProjectCard :project="project" />

            </div>
        </div>

        <!-- Pagination -->
        <nav v-if="lastPage" class="mt-4 d-flex justify-content-end" aria-label="Pagination">
            <ul class="pagination">
                <li class="page-item" :class="{ 'disabled': currentPage === 1 }">
                    <a @click.prevent=" getProjects(currentPage - 1)" class="page-link" href="#" aria-label="Previous">
                        <span aria-hidden="true">&laquo;</span>
                    </a>
                </li>
                <li class="page-item" v-for=" pageNum  in  lastPage " :class="{ 'active': currentPage === pageNum }"><a
                        @click.prevent="getProjects(pageNum)" class="page-link" href="#">{{ pageNum }}</a></li>

                <li class="page-item" :class="{ 'disabled': currentPage === lastPage }">
                    <a @click.prevent="getProjects(currentPage + 1)" class="page-link" href="#" aria-label="Next">
                        <span aria-hidden="true">&raquo;</span>
                    </a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>
