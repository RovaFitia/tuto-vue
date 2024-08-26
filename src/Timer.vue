<template>
    <div ref="div">
        Timer | {{ timer }} <br>
        Largeur: {{ size.width }}, Hauteur: {{ size.height }}
    </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

    const div = ref(null)
    const size = ref({width : 0 , height: 0})
    const timer = ref(0)
    let time
    onMounted(() => {
        const rect = div.value.getBoundingClientRect()
        size.value = {width: rect.width, height: rect.height}
        time = setInterval(()=> {
            console.log('Demo')
            timer.value++
        }, 1000)
    })

    onUnmounted(() => {
        clearInterval(time)
    })

</script>
