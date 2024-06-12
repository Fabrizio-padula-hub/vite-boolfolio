<script>
import axios from 'axios';

export default {
    name: 'SingleDetailsProject',
    data() {
        return {
            project: null
        };
    },
    methods: {
        getProjectFromApi() {
            axios.get(`http://127.0.0.1:8000/api/projects/${this.$route.params.slug}`)
            .then((response) => {
                this.project = response.data.results;

            });
        }
    },
    mounted() {
        this.getProjectFromApi();
    }
}
</script>

<template>
    <div v-if="project">
        
        <div class="card mt-3">
            <div class="card__border"></div>

            <!-- Nome projetto -->
            <div class="card_title__container">
                <h2 class="card_title">{{ project.name }}</h2>

                <!-- Nome cliente -->
                <span class="card_title">{{ project.client_name }}</span>

                <!-- Nome tipologia -->
                <div v-if="project.type" class="card_title">
                    <strong>Type</strong>:
                    {{ project.type.name }}
                </div>

                <!-- Nome tecnologia -->
                <div v-if="project.technologies.length > 0" class="card_title">
                    
                    <strong>Technologies</strong>:
                    <span v-for="tech in project.technologies" :class="tech.name === 'css' ? 'badge rounded-pill text-bg-info' : 'badge rounded-pill text-bg-success'">
                        {{ tech.name }}
                    </span>
                    
                </div>

                <!-- Immagine -->
                <div v-if="project.cover_image" class="mt-5">
                    <img class="img-thumbnail" :src="`http://127.0.0.1:8000/storage/${project.cover_image}`" alt="project.name">
                </div>

                <!-- Descrizione -->
                <p v-if="project.summary" class="card_paragraph mt-5">
                    {{ project.summary }}
                </p>
            </div>
    
         
        </div>

    </div>

</template>

<style scoped lang="scss">
.card {
    --white: hsl(0, 0%, 100%);
    --black: hsl(240, 15%, 9%);
    --paragraph: hsl(0, 0%, 83%);
    --line: hsl(240, 9%, 17%);
    --primary: hsl(266, 92%, 58%);

    position: relative;

    display: flex;
    flex-direction: column;
    gap: 1rem;

    padding: 1rem;
    background-color: hsla(240, 15%, 9%, 1);
    background-image: radial-gradient(at 88% 40%,
            hsla(240, 15%, 9%, 1) 0px,
            transparent 85%),
        radial-gradient(at 49% 30%, hsla(240, 15%, 9%, 1) 0px, transparent 85%),
        radial-gradient(at 14% 26%, hsla(240, 15%, 9%, 1) 0px, transparent 85%),
        radial-gradient(at 0% 64%, hsla(263, 93%, 56%, 1) 0px, transparent 85%),
        radial-gradient(at 41% 94%, hsla(284, 100%, 84%, 1) 0px, transparent 85%),
        radial-gradient(at 100% 99%, hsla(306, 100%, 57%, 1) 0px, transparent 85%);

    border-radius: 1rem;
    box-shadow: 0px -16px 24px 0px rgba(255, 255, 255, 0.25) inset;
}

.card .card__border {
    overflow: hidden;
    pointer-events: none;

    position: absolute;
    z-index: -10;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

    width: calc(100% + 2px);
    height: calc(100% + 2px);
    background-image: linear-gradient(0deg,
            hsl(0, 0%, 100%) -50%,
            hsl(0, 0%, 40%) 100%);

    border-radius: 1rem;
}

.card .card__border::before {
    content: "";
    pointer-events: none;

    position: fixed;
    z-index: 200;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%), rotate(0deg);
    transform-origin: left;

    width: 200%;
    height: 10rem;
    background-image: linear-gradient(0deg,
            hsla(0, 0%, 100%, 0) 0%,
            hsl(277, 95%, 60%) 40%,
            hsl(277, 95%, 60%) 60%,
            hsla(0, 0%, 40%, 0) 100%);

    animation: rotate 8s linear infinite;
}

@keyframes rotate {
    to {
        transform: rotate(360deg);
    }
}

.card .card_title__container .card_title {
    color: var(--white);
}

.card .card_title__container .card_paragraph {
    margin-top: 0.25rem;
 

    font-size: 0.9rem;
    color: var(--paragraph);
}

.card .line {
    width: 100%;
    height: 0.1rem;
    background-color: var(--line);

    border: none;
}

</style>