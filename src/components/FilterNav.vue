<template>
  <nav class="filterNav">
    <button :class="{'activeNav' : currentFilterVlaue == 'all'}" @click="filterBy('all')">All</button>
    <button :class="{'activeNav' : currentFilterVlaue == 'onGoing'}" @click="filterBy('onGoing')">OnGoing</button>
    <button :class="{'activeNav' : currentFilterVlaue == 'Complete'}" @click="filterBy('Complete')">Complete</button>
  </nav>
</template>

<script>
    export default {
        name: 'FilterNav',
        data() {
            return {
                currentFilterVlaue : "all"
            }
        },
        methods: {
            filterBy(byName) {
                this.$emit("filterValue",byName);
                this.currentFilterVlaue = byName;
            }
        },
    }
</script>

<style lang="scss" scoped>
.filterNav button{
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}
.activeNav {
    color: red !important;
}
</style>