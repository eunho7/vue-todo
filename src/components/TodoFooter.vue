<template>
    <div class="clearAllContainer">
        <span class="clearAllBtn" v-on:click="clearTodo">Clear All</span>
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            todoItems: []
        }
    },
    methods: {
        clearTodo () {
            localStorage.clear();
        }
    }
}
</script>

<style>
.clearAllContainer {
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background: white;
    border-radius: 5px;
    margin:0 auto;
}
.clearAllBtn {
    color: #e20303;
    display: block;
}
</style>