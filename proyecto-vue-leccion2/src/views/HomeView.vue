<template>
  <div class="container">
    <h1>App del clima mundial</h1>

    <!-- Dropdown para seleccionar ciudad -->
    <select v-model="selectedCity" @change="getWeather">
      <option disabled value="">Selecciona una ciudad</option>
      <option v-for="city in cities" :key="city.name" :value="city">
        {{ city.name }}
      </option>
    </select>

    <!-- Tarjeta de clima -->
    <WeatherCard
      v-if="weather"
      :city="selectedCity.name"
      :today="weather.today"
      :tomorrow="weather.tomorrow"
    />
  </div>
</template>

<script>
import cities from "../data/cities.json";
import WeatherCard from "../components/WeatherCard.vue";

export default {
  components: { WeatherCard },

  data() {
    return {
      cities,            // ciudades desde JSON
      selectedCity: "",  // ciudad seleccionada
      weather: null      // datos del clima
    };
  },

  methods: {
    // Obtiene clima desde Open-Meteo
    async getWeather() {
      const { lat, lon } = this.selectedCity;

      try {
        const res = await fetch(
          `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true&daily=temperature_2m_max&timezone=auto`
        );

        const data = await res.json();

        // Guardamos clima de hoy y mañana
        this.weather = {
          today: data.daily.temperature_2m_max[0],
          tomorrow: data.daily.temperature_2m_max[1]
        };

        console.log("Clima obtenido:", this.weather);
      } catch (error) {
        console.error("Error obteniendo clima", error);
      }
    }
  }
};
</script>

<style scoped>
.container {
  text-align: center;
  padding: 2rem;
}

select {
  padding: 0.5rem;
  margin-bottom: 1rem;
}
</style>
