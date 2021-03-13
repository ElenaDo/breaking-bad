<template>
  <v-container>
    <v-card
      class="mx-auto"
      max-width="600"
    >
    <v-card-title>List of Episodes</v-card-title>
    <v-card-subtitle v-show="!episodes.length" class="mt-3">
      There are no items to show</v-card-subtitle>
    <v-list>
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
