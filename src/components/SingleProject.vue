<script>
export default {
    name: 'SingleProject',
    props: {
        projectInfo: Object
    },
    methods: {
        truncateText(text) {
            if (text.length > 100) {
                return text.substr(0, 99) + '...';
            }

            return text;
        }
    }
}
</script>

<template>

    <div class="card my-3">
        <div class="card-body">
            <!-- titolo -->
            <div class="d-flex justify-content-between">
                <h4 class="card-title">
                    <strong>{{ projectInfo.name }}</strong>
                </h4>
                <div v-if="projectInfo.cover_image">
                    <i class="fa-solid fa-image"></i>
                </div>
            </div>


            <!-- tipologia -->
            <div v-if="projectInfo.type">
                <strong>tipo</strong>: {{ projectInfo.type.name }}
            </div>

            <!-- tecnologia -->
            <div v-if="projectInfo.technologies.length > 0">
                <strong>Tecnologie</strong><i class="fa-solid fa-gears"></i>:

                <span v-for="tech in projectInfo.technologies">
                    {{ tech.name }}
                    &nbsp
                </span>
            </div>

            <!-- descrizione -->
            <p v-if="projectInfo.summary" class="card-text mt-4">
                {{ truncateText(projectInfo.summary) }}
            </p>

            <!-- bottone -->
            <button class="my-btn">
                <router-link :to="{ name: 'single-project', params: { 'slug': projectInfo.slug } }"
                    class="btn btn-outline-success">
                    View More
                </router-link>
            </button>
        </div>
    </div>


</template>

<style scoped lang="scss">
p {
    color: rgb(148, 148, 148);
}

.my-btn {
    display: grid;
    place-items: center;
    background: #e3edf7;
    padding: 1.4em;
    border-radius: 10px;
    box-shadow: 6px 6px 10px -1px rgba(0, 0, 0, 0.15),
        -6px -6px 10px -1px rgba(255, 255, 255, 0.7);
    border: 1px solid rgba(0, 0, 0, 0);
    cursor: pointer;
    transition: transform 0.5s;
}

.my-btn:hover {
    box-shadow: inset 4px 4px 6px -1px rgba(0, 0, 0, 0.2),
        inset -4px -4px 6px -1px rgba(255, 255, 255, 0.7),
        -0.5px -0.5px 0px rgba(255, 255, 255, 1),
        0.5px 0.5px 0px rgba(0, 0, 0, 0.15),
        0px 12px 10px -10px rgba(0, 0, 0, 0.05);
    border: 1px solid rgba(0, 0, 0, 0.1);
    transform: translateY(0.5em);
}

.my-btn:hover svg {
    transform: scale(0.9);
    fill: #333333;
}
</style>