<script setup>
import { RouterView } from 'vue-router'
</script>

<template>
    <header>
      <nav>
        <div class="nav-left">
          <img src="@/assets/star_wars.png" alt="Star Wars Logo">
          <h1 class="view-title">List of Planets</h1>
        </div>
      </nav>
    </header> 

    <RouterView style="padding-top: 3.5em;"/>
</template>

<style scoped>
header {
  z-index: 9;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #333;
  color: #fff;
  padding: 10px 20px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.5);
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-left {
  display: flex;
  align-items: center;
}

.nav-left img {
  width: 90px;
  margin-right: 10px;
}

.view-title {
  margin: 0;
  font-size: 24px;
}
</style>
