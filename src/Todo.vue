<template>

    <button @click="showTimer = !showTimer">Afficher / Masquer</button>
    <Timer v-if="showTimer"/>

    <!-- <Layout>
        <template #header>
            En tête
        </template>

        <template #aside>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Id aliquid ea animi deserunt incidunt ratione similique sunt est consectetur itaque exercitationem illum tempora, enim repellendus explicabo numquam? Minus, ipsam! Consequatur!
        </template>

        <template #main>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Commodi minima explicabo expedita inventore harum voluptatem officia quidem, veritatis ab natus! Aliquid delectus beatae temporibus, repellat ratione ullam ea quas deserunt.
        </template>

        <template #footer>
            Pied de page
        </template>
    </Layout> -->
    <!-- <Button>Hello</Button> -->
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
    import {computed, onMounted, ref} from 'vue'
    import Checkbox from './Checkbox.vue'
    import Button from './Button.vue'
    import Layout from './Layout.vue'
    import Timer from './Timer.vue';

    const todos = ref([])
    const newTodo = ref('')
    const hideTodo = ref(false)
    const showTimer = ref(true)

    onMounted(()=> {
        fetch('https://jsonplaceholder.typicode.com/todos')
        .then(r => r.json())
        .then(v => todos.value = v.map(todo => ({ ...todo, date: todo.id})))
    })

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
