<template>
  <header>
      <img src="@/assets/logo.png" alt="pokeball" class="logo">
      <h1>Welcome</h1>
  </header>
</template>

<script>
export default {
    name: "TheHeader"
}
</script>

<style>
  header{
    display: flex;
    align-items: center;
    padding: .5em 1em;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(30, 60, 90, 0.1);

  }
  .logo{
    padding: .5em 1em;
  }

  img{
    width: 3em;
  }
</style>