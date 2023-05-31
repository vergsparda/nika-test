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
            <PersonList :list="personList" />
          </ul>
          <span class="no-list" v-show="!isShowPersonList">Пользователи не найдены</span>
        </div>
        <div class="favorites" v-show="isFavoriteActive">
          <div class="favorites-empty" v-show="!isAnyFavorite">
            <img src="../assets/empty-favorites.png" alt="" class="empty-fav-icon">
            <span class="empty-title">Список избранного пуст</span>
            <span class="empty-text">Добавляйте изображения, нажимая на звездочки</span>
          </div>
          <div class="favorites-list" v-if="isAnyFavorite">
            <FavoritePhoto
              v-for="photo in favorites"
              :key="photo.id"
              :photo="photo"/>
          </div>
        </div>
      </div>
    </div>
    <button class="popup" @click="handlePopup"></button>
  </div>
</template>

<script>
import PersonList from './personList.vue';
import FavoritePhoto from './favoritePhoto.vue';

export default {
  name: 'PhotoApp',
  props: {
    msg: String,
  },

  components: {
    PersonList,
    FavoritePhoto,
  },

  data() {
    return {
      personList: null,
      isCatalogActive: true,
      isFavoriteActive: false,
      isShowPersonList: false,
      isAnyFavorite: false,
      favorites: [],
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
      this.checkFavorites();
      this.isCatalogActive = false;
      this.isFavoriteActive = true;
    },

    switchToCatalog() {
      this.checkFavorites();
      this.isFavoriteActive = false;
      this.isCatalogActive = true;
    },

    handlePopup() {
      const popup = document.querySelector('.popup');
      popup.classList.toggle('active');
    },

    checkFavorites() {
      if (localStorage.getItem('favorites')) {
        this.favorites = JSON.parse(localStorage.getItem('favorites'));
        this.isAnyFavorite = true;
        return;
      }

      this.isAnyFavorite = false;
    },
  },

  mounted() {
    this.getPersonList('http://jsonplaceholder.typicode.com/users')
      .then((res) => {
        this.personList = res;
        this.isShowPersonList = true;
      });
    this.checkFavorites();
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

    &:disabled,
    &.disabled {
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

  .favorites {
    min-height: 710px;
    .favorites-empty {
      display: flex;
      flex-direction: column;
      padding: 250px 50px;
      align-items: center;

      .empty-fav-icon {
        width: 300px;
      }

      .empty-title {
        font-size: 23px;
        font-weight: 600;
        padding-top: 40px;
      }

      .empty-text {
        padding-top: 5px;
      }
    }

    .favorites-list {
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      margin: 0 auto;
      max-width: 530px;
      gap: 40px;
      padding: 40px 0;
    }
  }
}
</style>
