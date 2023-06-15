<script>
import axios from 'axios';
import { store } from "../store";

export default {
    name: "SingleProjectPage",
    data() {
        return {
            project: null,
            errorMessage: "",
            store
        }
    },
    mounted() {
        const slug = this.$route.params.slug;
        axios.get(`${store.apiBaseUrl}/api/projects/${slug}`).then(resp => {
            if (resp.data.success) {
                this.project = resp.data.results

            } else {

                this.errorMessage = `${slug} non è un progetto`
            }
        });
    }
}
</script>

<template>
    <section class="container">
        <router-link :to="{ name: 'projects' }" class="btn btn-success mb-3">Back</router-link>
        <div v-if="project">

            <h2>{{ project.title }}</h2>

            <div class="tags my-4">
                <span v-for="(technology, index) in project.technologys" :key="index">#{{ technology.name }}{{ index ===
                    project.technologys.length - 1 ? '' : ', '
                }}</span>
            </div>
            <p>
                {{ project.content }}
            </p>
        </div>
        <div v-else-if="errorMessage" class="my-4">

            {{ errorMessage }}
        </div>
    </section>
</template>

<style lang="scss" scoped></style>