<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    </v-app-bar>

    <v-main>
      <SelectForm :characters="characters" :selectedCharacters.sync="selectedCharacters" />
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';
import SelectForm from './components/SelectForm.vue';

export default {
  name: 'App',

  components: {
    SelectForm,
  },

  data: () => ({
    episodes: [],
    characters: [],
    selectedCharacters: [],
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
