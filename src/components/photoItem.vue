<template>
    <div class="photo-wrap">
      <button class="photo" @click="handlePhotoButton">
        <img
            class="photo-img"
            :src="photo.thumbnailUrl" :alt="photo.title">
      </button>
      <button class="favorite" @click="handleFavoriteButton">
        <img
          v-show="!isFavorite"
          class="fav-icon"
          src="../assets/icons-star.png"
          alt="">
          <!-- Хотел сделать один img и :src=" isFavorite ? одна звезда : другая"
            но картинку не видно, не стал разбираться для быстроты -->
          <img
          v-show="isFavorite"
          class="fav-icon"
          src="../assets/icons-star-filled.png"
          alt="">
      </button>
    </div>
  </template>

<script>
export default {
  name: 'photoItem',
  props: {
    photo: {
      type: Object,
      default() {
        return null;
      },
    },
  },

  data() {
    return {
      isOpen: false,
      photoList: null,
      isShowPhotos: false,
      favorites: [],
      isFavorite: false,
    };
  },

  methods: {
    handlePhotoButton() {
      const popup = document.querySelector('.popup');
      popup.classList.add('active');

      const popupImage = document.querySelector('.popup-image');
      if (popupImage) {
        popup.removeChild(popupImage);
      }

      const image = document.createElement('img');
      image.src = this.photo.url;
      image.alt = this.photo.title;
      image.classList.add('popup-image');
      image.style.borderRadius = '5px';

      popup.insertAdjacentElement('afterbegin', image);
    },

    handleFavoriteButton() {
      if (!this.isFavorite) {
        this.getLocalFavorites();
        this.favorites.push(this.photo);
        localStorage.setItem('favorites', JSON.stringify(this.favorites));
        this.isFavorite = true;
      } else {
        this.isFavorite = false;
        this.getLocalFavorites();

        if (this.favorites.length) {
          for (let i = 0; i < this.favorites.length; i += 1) {
            if (this.photo.id === this.favorites[i].id
              && this.photo.albumId === this.favorites[i].albumId) {
              this.favorites.splice(i, 1);
              localStorage.setItem('favorites', JSON.stringify(this.favorites));
            }
          }
        }
      }
    },

    checkFavorite() {
      if (this.favorites.length) {
        for (let i = 0; i < this.favorites.length; i += 1) {
          if (this.photo.id === this.favorites[i].id
              && this.photo.albumId === this.favorites[i].albumId) {
            this.isFavorite = true;
            return;
          }
          this.isFavorite = false;
        }
      }
    },

    getLocalFavorites() {
      if (localStorage.getItem('favorites')) {
        this.favorites = JSON.parse(localStorage.getItem('favorites'));
      }
    },
  },

  mounted() {
    this.getLocalFavorites();
    this.checkFavorite();
  },
};
</script>
  <style lang="scss" scoped>
  .photo-wrap {
    position: relative;
    .photo {
      height: 150px;
      width: 150px;
      padding: 0;
    }
    .photo-button {
      &:hover {
        background-color: #dae4ef;
      }
    }
    .photo-img {
      border-radius: 5px;
    }

    .favorite {
      position: absolute;
      z-index: 10;
      height: 35px;
      width: 35px;
      border-radius: 50%;
      right: 10px;
      top: 10px;
      background-color: #fff;
      display: flex;
      justify-content: center;
    }

    .fav-icon {
      width: 65%;
    }
  }

  </style>
