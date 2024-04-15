<template>
  <div class="bar">
    <input class="input" type="text" v-model="value" placeholder="Search" />
    <button class="btn" type="button" @click="$emit('changeQuery', value)">
      Search
    </button>
  </div>
</template>

<script>
export default {
  name: "search-bar",
  data() {
    return {
      value: "",
    };
  },
};
</script>

<style lang="css" scoped>
.bar {
  background-color: brown;
  height: 70px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.input {
  height: 40px;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
  padding-left: 10px;
  outline: none;
}
.btn {
  height: 38px;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
  padding: 0 7px;
  outline: none;
  border: none;
  transition: all 200ms linear;
}
.btn:hover,
.btn:focus {
  color: blueviolet;
  font-size: 15px;
  background-color: #6e6a6a;
}
</style>
