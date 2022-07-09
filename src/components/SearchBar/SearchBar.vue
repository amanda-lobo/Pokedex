<template>
  <div class="bodyInput">
    <input
      type="text"
      placeholder="Search"
      v-on:input="$emit('change', $event.target.value)"
    />
    <div class="hr"></div>
  </div>
</template>

<script>
import '../SearchBar/SearchBar.css';
export default {
  name: "SearchBar",
  data() {
    return { filter: null };
  },
  methods: {
    onFilter(e) {
      this.$emit('change', e.target.value);
    },
  },
};
</script>
