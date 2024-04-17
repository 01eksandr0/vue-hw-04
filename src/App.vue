<template>
  <div>
    <my-modal v-if="isVisible" :itSrc="isSrc" @close="isVisible = false" />
    <my-loader v-if="loading" />

    <search-bar @changeQuery="changeQuery" />
    <ul class="list">
      <li
        v-for="item in list"
        :key="item.id"
        @click="
          () => {
            isVisible = true;
            isSrc = item.urls.regular;
          }
        "
      >
        <photo-item :item="item" />
      </li>
    </ul>
    <button v-if="isBtn" @click="page = page + 1" class="btn">Load more</button>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import PhotoItem from "./components/PhotoItem.vue";
import MyModal from "./components/MyModal.vue";

import { getImages } from "./js/serchPhoto";
export default {
  components: { SearchBar, PhotoItem, MyModal },
  data() {
    return {
      query: "",
      list: [],
      page: 1,
      KEY: "tPyF-JOOf607yCQmy2T4mCANWSyx1bzc-VxDCaqrUmg",
      loading: false,
      isBtn: false,
      isVisible: false,
      isSrc: "",
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
      this.loading = true;
      try {
        const arrayImages = await getImages(searchParams);
        if (searchParams.page === 1) {
          this.list = arrayImages.data.results;
          this.isBtn = true;
        } else {
          this.list = [...this.list, ...arrayImages.data.results];
        }
      } catch (error) {
        console.log(error);
      } finally {
        this.loading = false;
      }
    },
    closeModalOnEscape(e) {
      if (e.key === "Escape") this.isVisible = false;
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
  mounted() {
    window.addEventListener("keydown", this.closeModalOnEscape);
  },
  destroyed() {
    window.removeEventListener("keydown", this.closeModalOnEscape);
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
.btn {
  padding: 4px 8px;
  background-color: red;
  font-size: 22px;
  color: #fff;
  margin-left: 700px;
}
</style>
