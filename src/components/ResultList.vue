<template>
  <v-container>
     <v-row>
      <v-col class="mx-auto" cols="12" sm="8" md="6">
        <v-card
          :loading="loading ? 'green darken-2' : null"
          class="mx-auto"
        >
        <v-card-title class="green--text text--darken-2">List of Episodes</v-card-title>
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
      </v-col>
     </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'resultList',
  props: { episodes: Array, loading: Boolean },
};
</script>
