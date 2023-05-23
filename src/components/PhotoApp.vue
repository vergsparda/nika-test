<template>
  <div class="wrap">
    <h1 class="title">{{ msg }}</h1>
    <div class="buttons">
        <button class="button" :class="{ active: isCatalogActive }" @click="switchToCatalog">
          Каталог
        </button>
        <button class="button" :class="{ active: isFavoriteActive }" @click="switchToFavorite">
          ☆ Избранное
        </button>
    </div>
    <div class="content">
      <div class="list" v-show="isCatalogActive"> List</div>
      <div class="favorites" v-show="isFavoriteActive">Favorites</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PhotoApp',
  props: {
    msg: String,
  },

  data() {
    return {
      personList: null,
      albumsList: null,
      photoList: null,
      albumsUrl: 'http://jsonplaceholder.typicode.com/albums?userId=3',
      photosUrl: 'http://jsonplaceholder.typicode.com/photos?albumId=21',
      isCatalogActive: true,
      isFavoriteActive: false,
    };
  },

  methods: {
    async getPersonList(url) {
      try {
        const response = await fetch(url);
        const list = response.json();
        return list;
      } catch (err) {
        console.log(`error ${err}`);
        return null;
      }
    },

    switchToFavorite() {
      this.isCatalogActive = false;
      this.isFavoriteActive = true;
    },

    switchToCatalog() {
      this.isFavoriteActive = false;
      this.isCatalogActive = true;
    },
  },

  mounted() {
    this.getPersonList('http://jsonplaceholder.typicode.com/users').then((res) => { this.personList = res; });
    // this.getDataList(this.albumsUrl).then((res) => { this.albumsList = res; });
    // this.getDataList(this.photosUrl).then((res) => { this.photoList = res; });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

.wrap {
  margin: 50px 0 ;
  max-width: 900px;
  margin: 0 auto 0;
  height: 100vh;

  .title {
    margin: 0;
    padding-top: 40px;
  }
  .content {
    // margin: 30px 0;
    background-color: #fff;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
    min-height: calc(100vh - 200px);
  }
  .buttons {
    display: flex;
    justify-content: center;
  }
  .button {
    margin-top: 20px;
    padding: 20px 0 20px;
    background-color: #a7c0d2;
    width: 100%;
    cursor: pointer;
    text-decoration: none;
    border: none;
    text-align: center;
    font-size: 16px;
    line-height: 16px;
    font-family: inherit;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;

    &:focus {
        outline: none;
    }

    &:disabled, &.disabled {
      cursor: not-allowed;
    }

    &.active {
      background-color: #fff;
    }
  }
}
</style>
