<!-- Gére les templates HTML (modèle) -->
<template>
    <!-- <p :id="`count-${count}`" :style="{color : count >= 5 ? 'red' : 'green'}" :class="{active: count > 5 }" >Compteur : {{ count }}</p>
    <div v-if="count >= 5">Vous avez cliquer plus de 5 fois</div>
    <div v-else>Vous avez cliquer moins de 5 fois</div>
    <button @click="increment">Incrément</button>
    <button @click="decrement">Décrément</button> -->

    <!-- Boucle avec Vue -->
    <!-- <hr/>
    <button @click="sortMovies">Réorganiser</button>

    <form action="" @submit.prevent="addMovie">
        <input type="text" placeholder="Enter your movie" v-model="movieName">
        <button>Add</button>
    </form>
    <ul>
        <li v-for="movie in movies" :key="movie">
            {{ movie }} <button @click="deleteMovie(movie)">Sup</button>
        </li>
    </ul> -->

    <ul>
        <li>{{ person.firstname }}</li>
        <li>{{ person.lastname }}</li>
        <li>{{ person.age }}</li>
    </ul>

    <button @click.prevent="changeAge">Changer l'age</button>

</template>

<!-- Gère les Javascript -->
<script setup>
import { ref } from 'vue';

const person = ref({
    firstname : 'Koto',
    lastname : 'Jean',
    age : 20
})

const changeAge = () => {
    person.value.age = Math.round(Math.random() * 100)
}


// const count = ref(0)

// const increment = ()=> {
//     count.value ++
// }

// const decrement = ()=> {
//     count.value --
// }

// // Tableau :
// const movies = ref([
//     'Matrix',
//     'Lilo & Stich',
//     'Avengers'
// ])

// const deleteMovie = (movie) => {
//     movies.value = movies.value.filter(m => m !== movie)
// }

// const sortMovies = () => {
//     // movies.value = movies.value.sort()
//     movies.value.sort((a,b) => a > b ? 1 : -1)
// }

// // Submit :
// const movieName = ref('')

// const addMovie = () => {
//     movies.value.push(movieName.value)
//     // vider le champ :
//     movieName.value = ""
// }

</script>

<!-- Gère les css -->
<style>
    .active {
        font-size: 1.5rem;
    }
</style>
