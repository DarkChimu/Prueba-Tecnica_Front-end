<template>
  <div class="profiles-section">
    <div class="wrapper">
      <div v-for="profile of profiles" :key="profile.id">
        <nuxt-link
          :to="{ name: 'details', params: { username: profile.login } }"
          class="profile-card centered"
        >
          <img class="mini-profile" :src="profile.avatar_url" alt="" />
          <p>{{ profile.login }}</p>
        </nuxt-link>
      </div>
    </div>
      <Chart class="profile-details" style="background-color: #fff":v-if="followersInfo.length" :datas="followersInfo" />
  </div>
</template>

<script>
import Chart from "../components/Chart.vue";
export default {
  name: "Profiles",
  components: {
    Chart,
  },
  data() {
    return {
      followersInfo: [['Seguidores', 'Cantidad']]
    };
  },
  watch: {
   'profiles' : function (){
       this.followersInfo = [['Seguidores', 'Cantidad']]
       this.getFollowers(this.profiles)
   }
  },
  mounted() {
      this.getFollowers(this.profiles)
  },
  props: {
    profiles: {
      type: Array,
      required: true,
      default: () => [],
    },
  },
  methods: {
    async getFollowers(usernames) {
        usernames.map(async username => {
            const response = (
                await this.$axios.get(`users/${username.login}`)
            ).data;

            this.followersInfo.push([response.login, response.followers]);
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.center-graphs {
  margin: 50px 42%;
}
</style>