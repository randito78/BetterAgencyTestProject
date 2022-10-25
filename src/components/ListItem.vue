<script>
export default {
  props: {
    item: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<template>
  <div>{{ this.item.id }}. {{ this.item.name }}</div>
</template>

<style scoped>
.thing {
  color: blue;
}
</style>
