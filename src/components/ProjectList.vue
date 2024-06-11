<script>
import axios from 'axios';
import SingleProject from './SingleProject.vue'


export default{
    name: 'ProjectList',
    components: {
        SingleProject
    },  
    data(){
        return{
            projects: []
        }
    },
    methods:{
        getPost(){
            axios.get('http://127.0.0.1:8000/api/projects')
            .then((response)=>{
                this.projects = response.data.results;
            });
        }
    },
    mounted() {
        this.getPost();
    }
}

</script>

<template>
    <h2>I Progetti</h2>
    <div class="row col-12">

        <SingleProject v-for="project in projects" :projectInfo="project" :key="project.id"></SingleProject>
        
    </div>
</template>

<style scoped lang="scss">

</style>