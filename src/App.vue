<script>
import AppHeader from './components/AppHeader.vue';

export default{
    components:{
        AppHeader
    }
}
</script>


<template>
    <AppHeader></AppHeader>

    <div class="container">
        <router-view></router-view>
    </div>
    
</template>


<style lang="scss">
@use './style/generic';
@use './style/partials/variables' as *;
</style>