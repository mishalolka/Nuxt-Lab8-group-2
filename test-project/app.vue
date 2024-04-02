<template>
  <div id="app">
    <nav>
      <a href="/students">Список студентів</a>
      <a href="/products">Список продуктів</a>
    </nav>
    <NuxtPage />
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}

nav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 60px;
  background-color: #f5f5f5;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}

nav a {
  text-decoration: none;
  color: #333;
  font-size: 18px;
  padding: 10px;
  border-radius: 5px;
}

nav a.router-link-active {
  background-color: #333;
  color: #fff;
}

main {
  padding: 20px;
}
</style>
