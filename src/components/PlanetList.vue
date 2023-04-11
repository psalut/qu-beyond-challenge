<script>
import PlanetItem from './PlanetItem.vue';
import axios from 'axios';

export default {
  name: 'PlanetList',
  data() {
    return {
      planets: [],
      loading: false,
      sortBy: 'population'
    }
  },
  methods: {
    getPlanets() {
      this.loading = true;
      axios.get('https://swapi.dev/api/planets/').then((planetsData) => {
        this.planets = planetsData.data.results;
        this.loading = false;
      })

    }
  },
  created() {
    this.getPlanets();
  },
  components: {
    PlanetItem,
  },
  computed: {
    sortedPlanets: function () {
      return this.planets.sort(function (a, b) {
        if (parseInt(a[this.sortBy]) < parseInt(b[this.sortBy])) {
          return -1;
        }
        if (parseInt(a[this.sortBy]) > parseInt(b[this.sortBy])) {
          return 1;
        }
        return 0;
      }.bind(this));
    }
  }
}
</script>

<template>
  <div class="row">
    
    <label for="planets-sort">Sort by: </label>
    <select v-model="sortBy" id="planets-sort">
      <option value="population">Population</option>
      <option value="diameter">Diameter</option>
      <!-- <option value="city">Ciudad</option> -->
    </select>
  </div>
  
  <div v-if="!loading">
    <div class="planet-list">
      <PlanetItem v-for="(planet, index) in sortedPlanets" :key="index" :planetData="planet"></PlanetItem>
    </div>
  </div>
  <div class="loader-container" v-if="loading">
    <div class="loader"></div>
  </div>
</template>

<style scoped>
  .loader-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.loader {
  border: 8px solid #333333;
  border-top: 8px solid #e9d515;
  border-radius: 50%;
  width: 60px;
  height: 60px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.planet-list {
  display: flex;
  flex-direction: column;
  margin: 10px 0;
}

.row {
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  align-items: center;
  width: 100%;
  margin: 0;
  padding: 0;
}

select {
  background-color: #f2f2f2;
  color: #444;
  padding: 5px;
  border-radius: 3px;
  border: none;
  font-size: 16px;
  margin-left: 5px;
}

select option:hover {
  background-color: #f2f2f2;
  color: #444;
  padding: 5px;
  border-radius: 3px;
  border: none;
  font-size: 16px;
  margin-left: 5px;
}

</style>