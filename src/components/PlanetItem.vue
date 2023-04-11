<template class="planet-item">
  <div class="planet-header" @click="isCollapsed = !isCollapsed">
    {{ planetData.name }}
  </div>
  <div class="planet-content" v-show="!isCollapsed">
    <div style="float:left; width: 50%">
      <p>Films:</p>
      <ul>
        <li v-for="(film, index) in this.films" :key="index">{{ film.title }}</li>
      </ul>
      <p >
      </p>
    </div>
    <div style="float:right; width: 50%;">
      <p> Population: {{ planetData.population }}</p>
      <p> Climate: {{ planetData.climate }}</p>
      <p> Gravity: {{ planetData.gravity }}</p>
      <p> Terrain: {{ planetData.terrain }}</p>
      <p> Diameter: {{ planetData.diameter }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  props: {
    planetData: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      films: Array,
      isCollapsed: true,
    }
  },
  created() {
    this.films = [];
    this.planetData.films.forEach(filmElement => {
      axios.get(filmElement).then((filmsData) => {
        this.films = [...this.films, filmsData.data];
      })
    });
    
  },
}
</script>

<style scoped>
.planet-item {
  background-color: #f5f5f5;
  border-radius: 5px;
  margin-bottom: 10px;
  overflow: hidden;
}

.planet-header {
  background-color: #ddd;
  font-weight: bold;
  padding: 10px;
}

.planet-header:hover {
  background-color: #e9d515;
  cursor: pointer;
}

.planet-content {
  padding: 10px;
}
</style>
