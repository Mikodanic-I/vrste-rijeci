<template>
  <v-combobox
    v-model="value"
    chips
    solo
    clearable
    multiple
    @click:clear="$emit('input', value)"
  >
    <template #selection="{attrs, item, select, selected}">
      <v-chip @click="openWordInDictionary(item.text)">
        <b>{{ item.text }}</b>
        &nbsp;
        <span>({{ item.tag }})</span>
      </v-chip>
    </template>
  </v-combobox>
</template>

<script>
export default {
  props: {
    value: {
      type: Array,
      required: false,
      default: () => []
    }
  },
  data() {
    return {
      chips: null
    };
  },
  methods: {
    openWordInDictionary(word) {
      window.open(`http://rjecnik.hr/search/?q=${word}`);
    }
  }
};
</script>
