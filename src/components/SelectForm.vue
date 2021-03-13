<template>
  <v-container>
    <v-row class="mt-3">
      <v-col class="mx-auto" cols="12" sm="8" md="6">
        <v-autocomplete
          color="green darken-2"
          item-color="green darken-2"
          @change="passCharList"
          v-model="selectedCharacters"
          :items="characters"
          item-text="name"
          outlined
          clearable
          dense
          label="Select characters"
          multiple
          :loading="loading"
        ></v-autocomplete>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'selectForm',
  props: { characters: Array, loading: Boolean },
  data: () => ({
    selectedCharacters: [],
  }),
  methods: {
    passCharList() {
      this.$emit('update:selectedCharacters', this.selectedCharacters);
    },
  },
};
</script>
