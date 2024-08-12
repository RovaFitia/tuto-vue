<!-- Gére les templates HTML (modèle) -->
<template>
    <h1>Bonjour {{ firstName.toUpperCase() }}</h1>
    <p>Comment ça va ?</p>
</template>

<!-- Gère les Javascript -->
<script setup>
    const firstName = "John Doe"
</script>

<!-- Gère les css -->
<style>
    h1 {
        color: red;
    }
</style>
