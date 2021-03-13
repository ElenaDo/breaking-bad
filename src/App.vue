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
      <ResultList :episodes="episodesByCharacters" />
    </v-main>
  </v-app>
</template>

<script>
import axios from 'axios';
import SelectForm from './components/SelectForm.vue';
import ResultList from './components/ResultList.vue';

export default {
  name: 'App',
  components: {
    SelectForm,
    ResultList,
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
      this.characters = this.getCharacters();
    },
    padString(str) {
      return str.trim().padStart(2, '0');
    },
    formatEpisodeName(episode) {
      const formatted = `S${this.padString(episode.season)}${this.padString(episode.episode)} - ${episode.title}`;
      return formatted;
    },
    getCharacters() {
      const characters = this.episodes.reduce((acc, curr) => {
        acc.push(...curr.characters);
        return acc;
      }, []);
      const uniqueCharacters = [...new Set(characters)];
      return uniqueCharacters;
    },
    breakingBad(query) {
      if (query.length === 0) return [];
      const { episodes } = this;
      const neededCharacters = (Array.isArray(query)) ? query : [query];
      const result = episodes.reduce((acc, curr) => {
        if (neededCharacters.every((character) => curr.characters.includes(character))) {
          acc.push(this.formatEpisodeName(curr));
        }
        return acc;
      }, []);
      return result;
    },
  },
};
</script>
