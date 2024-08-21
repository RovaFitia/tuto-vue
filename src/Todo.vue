<template>
    <Button>Hello</Button>
    <form action="" @submit.prevent="addTodos">
        <fieldset role="group">
            <input type="text" placeholder="Entrer votre tâche" v-model="newTodo">
            <button :disabled="newTodo.length === 0">Ajouter</button>
        </fieldset>
    </form>
    <div v-if="todos.length === 0">Vous n'avez pas fait aucune tâche :(</div>
    <div v-else>
        <ul>
            <li
                v-for="todo in sortTodo"
                :key="todo.date"
                :class="{completed : todo.completed}"
            >
                <!-- <label>
                    <input type="checkbox" v-model="todo.completed">
                    {{ todo.title }}
                </label> -->
                <!-- <Checkbox
                    :label="todo.title"
                    @check="console.log('coché')"
                    @uncheck="console.log('décoché')"
                /> -->

                <Checkbox
                    :label="todo.title"
                    v-model="todo.completed"
                />
            </li>
        </ul>

        <label>
            <input type="checkbox" v-model="hideTodo">
            Masquer les tâches complétées
        </label>

        <p v-if="remaningTodo > 0">
            {{ remaningTodo }} tâche{{ remaningTodo > 1 ? 's' : '' }} à faire
        </p>
    </div>

    <Checkbox label="Bonjour"/>

</template>

<script setup>
    import {computed, ref} from 'vue'
    import Checkbox from './Checkbox.vue'
    import Button from './Button.vue'

    const todos = ref([
        { "title": "Acheter la propriété 'Rue de la Paix'", "completed": false, "date": 20240730 },
        { "title": "Construire un hôtel sur 'Avenue Foch'", "completed": true, "date": 20240730 },
        { "title": "Éviter la case prison", "completed": false, "date": 20240730 }
    ])
    const newTodo = ref('')
    const hideTodo = ref(false)

    const addTodos = () => {
        todos.value.push({
            title: newTodo.value ,
            completed: false,
            date: Date.now()
        })

        newTodo.value = ""
    }

    // Order of todo :
    const sortTodo = computed(() => {
        console.log('Demo')
        const sortTodo = todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)

        if(hideTodo.value === true) {
            return sortTodo.filter(t => t.completed === false)
        }

        return sortTodo
    })

    const remaningTodo = computed(() => {
        return todos.value.filter(t => t.completed === false).length
    })
</script>

<style>
    .completed {
        opacity: .5;
        text-decoration: line-through;
    }
</style>
