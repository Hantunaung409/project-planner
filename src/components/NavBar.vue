<template>
    <div class="main-nav">
      <router-link to="/">Project</router-link>
      <router-link :to="{ name: 'addProject' }">Add Project</router-link>
    </div>
</template>

<script>
    export default {
        name: 'NavBar'
    }
</script>

<style lang="scss" scoped>
.main-nav{
    text-align: center;
    margin: 40px auto;
}
.main-nav a{
    display: -webkit-inline-flex;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
}
a.router-link-active {
    border-bottom: 2px solid #00cd89;
    padding-bottom: 4px;
}
</style>