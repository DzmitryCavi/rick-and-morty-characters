<template>
  <div>
    <div
      class="hacker-news-item"
      v-for="(item, $index) in list"
      :key="$index"
      :data-num="$index + 1">
      <router-link :to='`/${item.id}`'><div class="list_item">
        <span v-text="item.name"></span>
        <div class="list_item_img">
          <img :src="item.image" :alt="item.name">
        </div>
      </div></router-link>

    </div>
    <infinite-loading @infinite="infiniteHandler"></infinite-loading>
  </div>
</template>

<script>
import InfiniteLoading from 'vue-infinite-loading';
import axios from 'axios';

const api = 'https://rickandmortyapi.com/api/character/';

export default {
  name: 'List',
  components: {
    InfiniteLoading,
  },
  data() {
    return {
      page: 1,
      pagesCount: null,
      list: [],
      newsType: 'story',
    };
  },
  methods: {
    infiniteHandler($state) {
      if (this.pagesCount === this.page) {
        $state.complete();
      } else {
        axios.get(api, {
          params: {
            page: this.page,
          },
        }).then(({ data }) => {
          if (data.results.length) {
            this.page += 1;
            this.pagesCount = data.info.pages;
            this.list.push(...data.results);
            $state.loaded();
          } else {
            $state.complete();
          }
        });
      }
    },
  },
};
</script>

<style lang="scss">
.list_item {
  position: relative;
  margin: 15px auto;
  height: 100px;
  width: 80%;
  border: 0 solid #e5e5e5;
  overflow: hidden;
  display: block;
  cursor: pointer;
  background-color: rgb(255, 245, 245);
  box-shadow: 0 2px 2px 0 rgba(252, 252, 252, 0.5),
  0 0 0 3px rgba(255, 255, 255, 0.5);
  border-radius: 8px;
  text-indent: 20px;
  text-decoration: none;
  font-size: 3.5rem;
  font-family: "Ranchers", cursive;

  }
.list_item_img {
  right: 0;
  position: absolute;
  top: 0;
  img {
    height: 100px;
    width: 100px;
  }
}
a,
a:visited,
a:active {
  color: #0f0302;
  text-decoration:none;
}
a:hover {
  color: brown;
}
</style>
