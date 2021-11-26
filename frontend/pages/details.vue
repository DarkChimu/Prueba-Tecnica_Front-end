<template>
  <div>
      <nuxt-link class="go-back" to="/"> <button> Atrás </button></nuxt-link>
    <div class="profile-details">
      <div class="img">
        <img width="300px" :src="details.avatar_url" alt="" />
      </div>
      <div class="info">
        <h3>{{ details.login }}</h3>
        <p>Nombre: {{ details.name }}</p>
        <p>Biografía: {{ details.bio }}</p>
        <p>Localidad: {{ details.location }}</p>
        <p>Seguidores: {{ details.followers }}</p>
        <p>Siguiendo: {{ details.following }}</p>
        <p>Numero de Repositorios Publicos: {{ details.public_repos }}</p>
      </div>
      <div class="info" style="margin-top: 6px">
        <p>ID: {{details.id}}</p>
        <p>Compañía: {{ details.company }}</p>
        <p>
          Twitter:
          {{ details.twitter_username ? details.twitter_username : "No tiene" }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      details: {},
    };
  },
  created() {
    this.username = this.$route.params.username;
    this.getUser();
  },
  methods: {
    async getUser() {
      const response = (await this.$axios.get(`users/${this.username}`)).data;
      this.details = response;
    },
  },
};
</script>