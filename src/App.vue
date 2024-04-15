<template>
  <div>
    <my-loader />
    <search-bar @changeQuery="changeQuery" />
    <ul class="list">
      <li v-for="item in list" :key="item.id"><photo-item :item="item" /></li>
    </ul>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import PhotoItem from "./components/PhotoItem.vue";
import { getImages } from "./js/serchPhoto";
export default {
  components: { SearchBar, PhotoItem },
  data() {
    return {
      query: "",
      list: [],
      page: 1,
      KEY: "tPyF-JOOf607yCQmy2T4mCANWSyx1bzc-VxDCaqrUmg",
    };
  },
  methods: {
    changeQuery(newQuery) {
      if (!newQuery) return;
      this.query = newQuery;
    },
    async getPhoto() {
      if (!this.query) return;
      const searchParams = {
        query: this.query,
        client_id: this.KEY,
        page: this.page,
        per_page: 12,
      };
      try {
        const arrayImages = await getImages(searchParams);
        if (searchParams.page === 1) {
          this.list = arrayImages.data.results;
        } else {
          this.list.push([...images, ...arrayImages.data.results]);
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
  watch: {
    query() {
      this.getPhoto();
    },
    page() {
      this.getPhoto();
    },
  },
};
</script>

<style scoped>
.list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  margin-top: 20px;
}
.list > li {
  list-style: none;
}
</style>
