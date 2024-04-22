<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <img src="../src/assets/icondbapi.webp" alt="logo api dragonball">
      <nav>
        <RouterLink to="/">home</RouterLink>
        <RouterLink to="/result">results</RouterLink>
        <RouterLink to="/planet">planet</RouterLink>
        <button>Support us</button>
      </nav>
    </div>
  </header>
  <main>
    <RouterView />
  </main>
  <footer>
    <p>design by breta@bretzeldesign</p>
  </footer>
</template>



<style scoped>
header {
  line-height: 1.5;
  background-color: rgb(255, 255, 255);
  padding: 10px;
  border-radius: 0rem 0rem 0.5rem 0.5rem;
}
header img{
  width: 60px;
  height: auto;
}
.wrapper{
  display: flex;
  justify-content: center;
  align-items: center;
}
nav {
  width: 100%;
  font-size: 20px;
  text-align: end;
  display: flex;
  justify-content: end;
  color: var(--color-text);
}
nav button{
  background-color: rgb(251, 192, 45);
  color: #fff;
  border: 0;
  border-radius: 0.2rem;
  height: 35px;
  width: 150px;
  font-size: 20px;
  font-weight: 500;
  padding: 6px 16px;
}
nav a{
  color: var(--color-text);
  font-weight: 900;
  line-height: 1.6;
  font-size: 20px;
  display: inline-block;
  padding: 0 2rem;
}
nav a:hover {
  background-color: transparent;
}
nav a:first-of-type {
  border: 0;
}
footer{
  text-align: center;
  padding: 20px;
}

</style>
