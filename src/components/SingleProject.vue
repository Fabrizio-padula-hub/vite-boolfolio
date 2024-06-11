<script>
export default{
    name: 'SingleProject',
    props: {
        projectInfo: Object
    },
    methods:{
        truncateText(text){
            if(text.length >100){
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
            <h5 class="card-title">{{ projectInfo.name }}</h5>
            <div v-if="projectInfo.type">
                <strong>tipo</strong>: {{ projectInfo.type.name }}
            </div>
            <div v-if="projectInfo.technologies.length > 0">
                <strong>Tecnologie</strong>:
                <span v-for="tech in projectInfo.technologies">
                    {{ tech.name }}
                &nbsp</span>
            </div>
            <p v-if="projectInfo.summary" class="card-text mt-4">{{ truncateText(projectInfo.summary) }}</p>
            <!-- <a href="#" class="btn btn-primary">Go somewhere</a> -->
        </div>
    </div>

  
</template>