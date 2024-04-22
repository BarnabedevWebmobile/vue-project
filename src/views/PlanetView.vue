<script setup>
    import planet from '../components/planet.vue';
</script>

<template>

    <button class="reset" v-on:click="getAnswer()">
        showplanet
    </button>

    <ul class="listeperso" v-if="Listeplanet">
        <planet :planet="planet" v-for="(planet, index) in Listeplanet.items"/>
    </ul>
    
</template>

<script>
import axios from "axios";

export default {
// données vérifier dans le document
    data() {
    return {

        Listeplanet:{},
        showplanet:false

    };
    },
    methods: {
    async getAnswer() {
        const { data } = await axios.get("https://dragonball-api.com/api/planets?limit=20");
        this.Listeplanet = data;
        console.log(this.Listeplanet)
        this.showplanet = true
        },
    },

};
</script>

