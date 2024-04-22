<script setup>
    defineProps({
        planet: Object
    })
</script>


<template>
    <li class="planet">
        <div class="image"  v-bind:style="{ backgroundImage: 'url(' +planet.image+ ')' }">
        </div>
        <div class="content">
            <h3>{{ planet.name }}</h3>
        </div>
    </li>
</template>

<style scoped>
    .planet .image{
        width: auto;
        margin: auto;
        transition: all .3s;
        height: 250px;
        width: 100%;
    }
</style>