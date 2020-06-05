<template>
  <v-container fill-height>
    <v-row justify="center">
      <h1 class="display-3">Vrste riječi</h1>
    </v-row>
    <v-row justify="center">
      <v-text-field
        v-model="sentence"
        placeholder="Upišite rečenicu"
        rounded
        outlined
        append-icon="search"
        @keydown.enter="fetchWordTypes"
        @click:append="fetchWordTypes"
      />
    </v-row>
    <chips-list v-model="words" @input="sentence = null" />
    <v-row align="bottom" justify="center">
      API je napravio Croapi
    </v-row>
  </v-container>
</template>

<script>
import chipsList from "../components/chipsList";
export default {
  components: {
    chipsList
  },
  data() {
    return {
      sentence: null,
      words: []
    };
  },
  methods: {
    async fetchWordTypes() {
      try {
        const { data } = await this.$axios.post(
          "https://cors-workaround-api.herokuapp.com/cors",
          {
            method: "POST",
            url:
              "https://y23blf12y4.execute-api.eu-central-1.amazonaws.com/prod/pos",
            headers: {
              "x-api-key": "TwWmLpW0Xj9Kkheo5UpHB6c01ZR7RxAd3BZyfLmS"
            },
            data: {
              sentence: this.sentence
            }
          }
        );
        this.words = data.apiResponse.words;
      } catch (e) {}
    }
  }
};
</script>
