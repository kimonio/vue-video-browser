<template>
  <div>
    <input @input="onInput"/>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  methods: {
    onInput(e) {
      this.$emit('term-change', e.target.value);
    }
  }
}
</script>

<style>

</style>