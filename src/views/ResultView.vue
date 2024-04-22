<script setup>

    import Winner from '../components/Winner.vue'

</script>

<template>
    <h1>Resultats</h1>
    <Winner :winner ="localwinner" :perso1="localperso1" :perso2="localperso2"/>
</template>

<script>

    export default{

        data() {
            return {
                localwinner: '',
                localperso1: '',
                localperso2: ''
            };
        },
        mounted(){
            this.localwinner = localStorage.getItem('winner'),
            this.localperso1 = localStorage.getItem('combatant1'),
            this.localperso2 = localStorage.getItem('combatant2')
            console.log(this.localwinner)
        }
    }
    
</script>