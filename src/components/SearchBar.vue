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

<style>
* {
  border: 0;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.bodyInput {
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
input {
  padding: 5px;
  margin: 5px;
  background-color: #ededed;
  outline-style: none;
  width: 98%;
}
.hr {
  width: 98%;
  height: 1px;
  background-color: #cacaca;
}
</style>
