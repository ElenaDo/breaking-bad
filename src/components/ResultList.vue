<template>
  <v-container>
    <v-card
      class="mx-auto"
      max-width="600"
    >
    <v-card-title>List of Episodes</v-card-title>
    <v-list dense>
      <v-list-item
          v-for="(episode) in episodes"
          :key="episode"
        >
        {{ episode }}
      </v-list-item>
    </v-list>

    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'resultList',
  props: { episodes: Array },
};
</script>
