<template>
  <div class="container" @click="$emit('close')">
    <img @click.stop class="img" :src="itSrc" alt="" />
  </div>
</template>

<script>
export default {
  name: "my-modal",
  props: {
    itSrc: String,
  },
};
</script>

<style lang="css" scoped>
.container {
  position: fixed;
  height: 100%;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}
.img {
  height: 500px;
  width: 600px;
}
</style>
