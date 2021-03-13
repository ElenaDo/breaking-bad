<template>
  <v-container>
    <v-row>
      <v-col class="mx-auto" cols="12" sm="8" md="6">
        <v-autocomplete
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
