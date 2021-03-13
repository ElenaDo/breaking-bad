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
      <ul>
        <li v-for="episode in episodesByCharacters" :key="episode">
          {{ episode }}
        </li>
      </ul>
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
  computed: {
    episodesByCharacters() {
      const result = this.breakingBad(this.selectedCharacters);
      return result;
    },
  },
  mounted() {
    this.getCharacterList();
    this.getEpisodeList();
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
    padString(str) {
      return str.trim().padStart(2, '0');
    },
    formatEpisodeName(episode) {
      const formatted = `S${this.padString(episode.season)}${this.padString(episode.episode)} - ${episode.title}`;
      return formatted;
    },
    breakingBad(query) {
      const { episodes } = this;
      const neededCharacters = (Array.isArray(query)) ? query : [query];
      const result = episodes.reduce((acc, curr) => {
        if (neededCharacters.every((character) => curr.characters.includes(character))) {
          acc.push(this.formatEpisodeName(curr));
        }
        return acc;
      }, []);
      console.log(result.length, query.length);
      return result;
    },
  },
};
</script>
