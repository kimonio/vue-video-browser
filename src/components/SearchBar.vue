<template>
  <div>
    <input @keyup.enter="onChange" />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  methods: {
    onChange(e) {
      this.$emit("term-change", e.target.value);
    },
  },
};
</script>

<style scoped>
input {
  width: 75%;
}

div {
  text-align: center;
  margin: 20px;
}
</style>
