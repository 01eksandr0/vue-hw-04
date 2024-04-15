<template>
  <div>
    <img :src="item.urls.regular" height="220" width="300" />
  </div>
</template>

<script>
export default {
  name: "photo-item",
  props: {
    item: Object,
  },
};
</script>

<style lang="scss" scoped></style>
