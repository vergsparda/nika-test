<template>
  <div class="wrap">
    <h1 class="title">{{ msg }}</h1>
    <div class="body">
      <div class="buttons">
          <button class="button" :class="{ active: isCatalogActive }" @click="switchToCatalog">
            Каталог
          </button>
          <button class="button" :class="{ active: isFavoriteActive }" @click="switchToFavorite">
            ☆ Избранное
          </button>
      </div>
      <div class="content">
        <div class="persons" v-show="isCatalogActive">
          <ul class="list" v-show="isShowPersonList">
            <PersonList  :list="personList"/>
          </ul>
          <span class="no-list" v-show="!isShowPersonList">Пользователи не найдены</span>
        </div>
        <div class="favorites" v-show="isFavoriteActive">Favorites</div>
      </div>
    </div>
    <button class="popup" @click="handlePopup"></button>
  </div>
</template>

<script>
import PersonList from './personList.vue';

export default {
  name: 'PhotoApp',
  props: {
    msg: String,
  },

  components: {
    PersonList,
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
      isShowPersonList: false,
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

    handlePopup() {
      const popup = document.querySelector('.popup');
      popup.classList.toggle('active');
    },
  },

  mounted() {
    this.getPersonList('http://jsonplaceholder.typicode.com/users')
      .then((res) => {
        this.personList = res;
        this.isShowPersonList = true;
      });
  },
};
</script>

<style lang="scss" scoped>

.wrap {
  position: relative;
  max-width: 900px;
  margin: 0 auto;
  padding-bottom: 30px;

  .title {
    margin: 0;
    padding-top: 40px;
  }
  .body {
    box-shadow: 0px 10px 10px 0px rgba(0, 0, 0, 0.5);
    border-radius: 10px;
  }
  .content {
    background-color: #fff;
  }
  .buttons {
    display: flex;
    justify-content: center;
  }
  .button {
    padding: 20px 0 20px;
    background-color: #a7c0d2;
    font-size: 16px;
    line-height: 16px;
    justify-content: center;
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

  .popup {
        position: fixed;
        display: none;
        width: 100%;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 20;
        justify-content: center;
        align-items: center;
        background: rgba(0, 0, 0, .8);

        &.active {
            display: flex;
        }
    }
}
</style>
