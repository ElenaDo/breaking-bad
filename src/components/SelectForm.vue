<template>
  <v-app>
    <v-container>
      <v-row>
        <v-col class="mx-auto" cols="12" md="6">
          <v-autocomplete
            v-model="neededCharacters"
            :items="characters"
            item-text="name"
            outlined
            dense
            label="Characters"
            multiple
          ></v-autocomplete>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
export default {
  name: 'selectForm',
  props: { characters: Array },
  data: () => ({
    neededCharacters: [],
  }),
};
</script>
