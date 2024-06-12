<script>
import axios from 'axios';
import SingleProject from '../components/SingleProject.vue'


export default {
    name: 'ProjectList',
    components: {
        SingleProject
    },
    data() {
        return {
            projects: [],
            currentPage: 1,
            nextPageUrl: null,
            prevPageUrl: null
        }
    },
    methods: {
        getPost(dataPage) {
            axios.get('http://127.0.0.1:8000/api/projects', {
                params: {
                    page: dataPage
                }
            })
                .then((response) => {
                    this.projects = response.data.results.data;
                    this.currentPage = response.data.results.current_page;
                    this.nextPageUrl = response.data.results.next_page_url;
                    this.prevPageUrl = response.data.results.prev_page_url

                });
        }
    },
    mounted() {
        this.getPost(this.currentPage);
    }
}

</script>

<template>
    <h1>Progetti</h1>

    <div class="row col-12">

        <SingleProject v-for="project in projects" :projectInfo="project" :key="project.id"></SingleProject>

    </div>
    <nav aria-label="Page navigation example">
        <ul class="pagination justify-content-between">
            <li v-if="prevPageUrl" class="page-item">
                <button @click="getPost(currentPage - 1)">
                    <span aria-hidden="true">Previous</span>
                </button>
            </li>
         
            <li v-if="nextPageUrl" class="page-item">
                <button @click="getPost(currentPage + 1)">
                    <span aria-hidden="true">Next</span>
                </button>
            </li>
        </ul>
    </nav>
</template>

<style scoped lang="scss">
button {
  color: #090909;
  padding: 0.7em 1.7em;
  font-size: 18px;
  border-radius: 0.5em;
  background: #e8e8e8;
  cursor: pointer;
  border: 1px solid #e8e8e8;
  transition: all 0.3s;
  box-shadow: 6px 6px 12px #c5c5c5, -6px -6px 12px #ffffff;
}

button:active {
  color: #666;
  box-shadow: inset 4px 4px 12px #c5c5c5, inset -4px -4px 12px #ffffff;
}


</style>