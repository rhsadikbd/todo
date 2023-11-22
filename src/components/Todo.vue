<!-- Script Files -->
<script setup>
import { ref, reactive } from 'vue';


const title = ref('Todo List')
let isTodo = ref(true)
let newTodo = ref('')
const todos = reactive([])
const changeStatus = (params) => {
    if (params == 'add') {
        isTodo.value = false
    }
    if (params == 'remove') {
        isTodo.value = true
    }
}
const addItem = () => {
    const item = newTodo.value
    const newItem = {
        id: todos.length + 1,
        text: item
    }
    todos.push(newItem)
    newTodo.value = ''
}
const removeTodo = (index) => {
    todos.splice(index, 1)
}
</script>
<!-- End Script Files -->





<!-- Template Files -->
<template>
    <main class="h-screen bg-cover flex justify-center items-center">
        <div class="bg-white w-96 rounded-md h-96 shadow-2xl">
            <div class="flex items-center justify-between p-4 gap-2">
                <h1 v-if="isTodo" class="text-2xl font-bold text-slate-500">{{ title }}</h1>
                <input v-else v-model="newTodo" @change.enter="addItem" type="text" placeholder="What to do?"
                    class="w-full bg-slate-200 h-10 px-3 focus:border-1 focus:border-slate-600">
                <svg v-if="isTodo" @click="changeStatus('add')" xmlns="http://www.w3.org/2000/svg" fill="none"
                    viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                    class=" w-10 bg-green-100 p-2 cursor-pointer select-none active:bg-green-200">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
                </svg>
                <svg v-else @click="changeStatus('remove')" xmlns="http://www.w3.org/2000/svg" fill="none"
                    viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                    class=" w-11 bg-red-100 p-2 cursor-pointer select-none active:bg-red-200">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 12h-15" />
                </svg>
            </div>
            <div class="border-2 border-slate-400 text-center mx-4 py-2" v-if="todos.length == 0">
                <h3>Nothing to show</h3>
            </div>
            <ul class="list-none custom-lists overflow-y-auto h-72">
                <li class="flex justify-between items-center px-4 py-2 transition-opacity"
                    v-for="(listItem, index) in todos" :key="index">
                    <label class="flex gap-2 text-md" :for="`item${index}`">
                        <input type="checkbox" :id="`item${index}`" v-model="todos[index].completed">
                        <span class="text-slate-700" :class="{ 'completed': todos[index].completed }">{{
                            listItem.text
                        }}</span>
                    </label>
                    <svg xmlns="http://www.w3.org/2000/svg" @click="removeTodo(index)" fill="none" viewBox="0 0 24 24"
                        stroke-width="1.5" stroke="currentColor"
                        class="remove w-5 cursor-pointer select-none text-red-500 active:text-red-700 transition-opacity">
                        <path stroke-linecap="round" stroke-linejoin="round"
                            d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                    </svg>
                </li>
            </ul>
        </div>

    </main>
</template>
<!-- End Template Files -->




<!-- Style Files -->
<style scoped lang="scss">
main {
    background-image: url('../assets/images/todo-bg.jpg');

    .custom-lists {
        li {
            .remove {
                opacity: 0;
            }

            &:hover {
                .remove {
                    opacity: 1;
                }
            }
        }
    }

    .completed {
        text-decoration: line-through;
        color: #8b8b8b;
    }


}
</style>
<!-- End Style Files -->
