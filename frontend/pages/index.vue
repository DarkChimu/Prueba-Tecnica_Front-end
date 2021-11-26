<template>
  <div>
    <div class="search-section">
      <input type="text" v-model="search" placeholder="Ej: Jonh Connor" @change="clearErrors">
      <button @click="searchProfiles">Buscar</button>
    </div>
    <p class="error" v-if="errors.length">
      <ul>
        <li v-for="error in errors" :key="error">{{ error }}</li>
      </ul>
    </p>
    <Profiles v-if="profilesData.length" :profiles="profilesData"/>
    <div v-else>
      <h3 class="text-center">No se encontraron resultados</h3>
    </div>
  </div>
</template>

<script>
import Profiles from "../components/Profiles.vue";
export default {
  components: {
    Profiles,
  },
  data() {
    return {
      profilesData: [],
      search: "",
      errors: [],
    };
  },
  methods: {
    async searchProfiles() {
      if (this.search.length < 3) {
        this.errors = ["El nombre de usuario debe tener al menos 4 caracteres"];
        return
      }else if (this.search === 'iseijasunow') {
        this.errors = ["El nombre de usuario no puede ser iseijasunow"];
        return
      }

      const response = (
        await this.$axios.get(`search/users?q=${this.search}&per_page=12`)
      ).data;
      this.profilesData = response.items;
    },
    clearErrors() {
      this.errors = [];
    }
  },
};
</script>