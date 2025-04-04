<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Chart from 'chart.js/auto';
import { onMounted, ref } from 'vue'


</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="http://media.smapply.io/media/assets2/reviewrooms/smallbusinessservice/logo/SBS_NDD_LOGO.png" width="425" height="125" />

    <div class="wrapper">
      <HelloWorld msg="Small Business Services in New York City" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/bar">Bar</RouterLink>
        <RouterLink to="/pie">Pie</RouterLink>
      </nav>
    </div>
  
  </header>
  <RouterView />

</template>

<style scoped>
header {
  line-height: 1;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 16spx;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    flex-direction: column;
    place-items: center;
    margin: 80px;
  }

  .logo {
    margin: 0 0 3rem;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    align-items: center;
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
