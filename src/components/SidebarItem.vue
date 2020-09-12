<template>
  <button
    class="sidebar-item"
    @click="handleClick($event, index)"
    :class="{active: active}"
  >{{ option.name }}</button>
</template>

<script>
export default {
  name: "Sidebar Item",
  props: ["option", "active", "index"],
  methods: {
    handleClick(event, index) {
      this.$emit("handleClick", index);
    },
  },
};
</script>

<style scoped>
</style>