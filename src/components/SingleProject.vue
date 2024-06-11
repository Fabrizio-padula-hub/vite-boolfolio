<script>
export default{
    name: 'SingleProject',
    props: {
        projectInfo: Object
    }
}
</script>

<template>

    <div class="card my-3">
        <img src="..." class="card-img-top" :alt="projectInfo.name">
        <div class="card-body">
            <h5 class="card-title">{{ projectInfo.name }}</h5>
            <p v-if="projectInfo.summary" class="card-text">{{ projectInfo.summary }}</p>
            <!-- <a href="#" class="btn btn-primary">Go somewhere</a> -->
        </div>
    </div>

  
</template>