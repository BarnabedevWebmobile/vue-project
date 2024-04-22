<script setup>
    defineProps({
    perso1: Array,
    perso2: Array,
    winner: Array
    })
</script>

<template>
    <h2>winner</h2>
    <br>
    <h3>fighter :</h3>
    <div class="fight">
        <span class="data">
            <div class="image">
                <img  :src="perso1.image" :alt="perso1.name">
            </div>
            <div class="content">
            <h4>
            nom
            </h4>
            <p>ki :</p>
            </div>
        </span>
        <span class="data">
            <div class="image">
                <img  :src="perso2.image" :alt="perso2.name">
            </div> 
            <div class="content">
            <h4>
            nom
            </h4>
            <p>ki :</p>
            </div>
        </span>
        <span class="data">
            <div class="image">
                <img  :src="winner.image" :alt="winner.name">
            </div>
            <div class="content">
            <h4>
            winner :nom
            </h4>
            <p>ki :</p>
            </div>

        </span>
    </div>


</template>

<style scoped>

.fight{
    display: flex;
}
.data{
    width: 450px;
    height: 580px;
    margin: 25px;
    border-radius: 0.4rem 1.5rem 0.4rem 1.5rem;
    border: 1px solid rgba(84, 84, 84, 0.75);
    background-color: rgba(84, 84, 84, 0.65);
}
.image{
  display: flex;
  background-image: url(../assets/89980.webp);
  background-size: cover;
  border-radius: 0.4rem 1.5rem 0rem 0rem;
}

.image img{
  height: 250px;
}

.image img{
  width: auto;
  margin: auto;
  transition: all .3s;
}
.image img{
  height: 450px;
}

.image img:hover{
  transform: scale(1.5);
}


</style>