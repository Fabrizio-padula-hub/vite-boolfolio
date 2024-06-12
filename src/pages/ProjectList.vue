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
            projects: []
        }
    },
    methods: {
        getPost() {
            axios.get('http://127.0.0.1:8000/api/projects')
                .then((response) => {
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
    <button class="button mt-4" data-text="Awesome">
        <span class="actual-text">&nbsp;progetti&nbsp;</span>
        <span aria-hidden="true" class="hover-text">&nbsp;progetti&nbsp;</span>
    </button>
    <div class="row col-12">

        <SingleProject v-for="project in projects" :projectInfo="project" :key="project.id"></SingleProject>

    </div>
</template>

<style scoped lang="scss">
/* === removing default button style ===*/
.button {
    margin: 0;
    height: auto;
    background: transparent;
    padding: 0;
    border: none;
    cursor: none;
}

/* button styling */
.button {
    --border-right: 6px;
    --text-stroke-color: rgba(255, 255, 255, 0.6);
    --animation-color: #37FF8B;
    --fs-size: 2em;
    letter-spacing: 3px;
    text-decoration: none;
    font-size: var(--fs-size);
    font-family: "Arial";
    position: relative;
    text-transform: uppercase;
    color: transparent;
    -webkit-text-stroke: 1px var(--text-stroke-color);
}

/* this is the text, when you hover on button */
.hover-text {
    position: absolute;
    box-sizing: border-box;
    content: attr(data-text);
    color: var(--animation-color);
    width: 0%;
    inset: 0;
    border-right: var(--border-right) solid var(--animation-color);
    overflow: hidden;
    transition: 0.5s;
    -webkit-text-stroke: 1px var(--animation-color);
}

/* hover */
.button:hover .hover-text {
    width: 100%;
    filter: drop-shadow(0 0 23px var(--animation-color))
}
</style>