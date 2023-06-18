<script>
import axios from 'axios';
import ProjectCard from '../components/ProjectCard.vue';
import { store } from '../store';


export default {
    name: "ProjectsPage",

    data() {
        return {
            projects: [],
            currentPage: 1,
            lastPage: null,
            totalProjects: 0,
            types: [],
            selectedType: "all",
            store
        };

    },
    mounted() {
        this.getProjects();
        this.getTypes();

    },
    methods: {
        getTypes() {
            axios.get(`${store.apiBaseUrl}/api/types`).then((resp) => {
                this.types = resp.data.results;
            })
        },
        getProjects(pageNumber = 1) {

            const params = {
                page: pageNumber,

            }

            if (this.selectedType !== "all") {

                params.type_id = this.selectedType;

            }
            axios.get(`${store.apiBaseUrl}/api/projects`, { params }).then(resp => {
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

        <!-- Filtri -->
        <p>
            <label class="form-label" for="category">Tipi</label>
            <select v-model="selectedType" id="category" class="form-select" @change="getProjects()">
                <option value="all">Tutti</option>
                <option :value="singleType.id" v-for="singleType in types" :key="singleType.id">{{ singleType.name }}
                </option>
            </select>
        </p>

        <h5 class="m-3 text-end">Progetti totali: {{ totalProjects }}</h5>
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

<style lang="scss" scoped></style>