<template>
  <div id="app">
    <TheHeader />
      <main>
        <TheList />
      </main>
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue'
import TheList from './components/TheList.vue'

export default {
  name: 'App',
  components: {
    TheHeader,
    TheList,
  }
}
</script>

<style>
body, ul, li, h1, h2, p {
  padding: 0;
  margin: 0;
  list-style: none;
}

body{
  background: url("./assets/pattern.svg") repeat top;
}

img {
  max-width: 100%;
  display: block;
}

#app {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #232528;
}

#main {
  flex: 1;
}

</style>
