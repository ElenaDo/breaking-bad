<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    </v-app-bar>

    <v-main>
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    episodes: [],
    characters: [],
  }),
  mounted() {
    this.getEpisodeList();
    this.getCharacterList();
  },
  methods: {
    async request(path = '') {
      let result;
      try {
        const host = process.env.VUE_APP_HOST;
        result = await axios(host + path);
      } catch (err) {
        console.error(err);
      }
      return result.data;
    },
    async getEpisodeList() {
      this.episodes = await this.request('episodes');
    },
    async getCharacterList() {
      this.characters = await this.request('characters');
    },
  },
};
</script>
