<script setup>
    defineProps({
    perso: Object,
    frombattle: String 
    })
</script>

<template>
  <li>
    <div class="image">
      <img v-if="perso.image" :src="perso.image" :alt="perso.name">
    </div>
    <div class="content">
      <h3>{{ perso.name }}
      </h3><p>{{ perso.race }} - {{ perso.gender }}</p><br/>
      <span v-if="frombattle == 'true'"><h4>base KI: </h4><br><p>{{ perso.ki }}</p><br/></span>
      <h4>affiliation: </h4><p>{{ perso.affiliation }}</p>
    </div>
  </li>
</template>