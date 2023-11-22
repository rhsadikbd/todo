<template>
    <Todo></Todo>
</template>

<script setup>
import Todo from './components/Todo.vue'
</script>

<style lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

::-webkit-scrollbar {
    width: 10px;
}

::-webkit-scrollbar-thumb {
    background-color: rgb(167, 255, 167);
}

::-webkit-scrollbar-track {
    background-color: rgb(226, 255, 226);
}
</style>