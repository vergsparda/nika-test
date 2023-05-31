<template>
        <div class="photo-wrap" v-show="isFavorite">
            <button class="photo" @click="handlePhotoButton">
                <img class="photo-img" :src="photo.thumbnailUrl" :alt="photo.title">
            </button>
            <button class="favorite" @click="handleFavoriteButton">
                <img
                    class="fav-icon"
                    src="../assets/icons-star-filled.png"
                    alt="">
            </button>
            <span class="photo-text">{{ photo.title }}</span>
        </div>
</template>
<script>
export default {
  name: 'favoritePhotoItem',
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
      isFavorite: true,
      favorites: [],
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
      const favorites = JSON.parse(localStorage.getItem('favorites'));

      if (favorites.length > 1) {
        for (let i = 0; i < favorites.length; i += 1) {
          if (this.photo.id === favorites[i].id
                    && this.photo.albumId === favorites[i].albumId) {
            favorites.splice(i, 1);
            localStorage.setItem('favorites', JSON.stringify(favorites));
          }
        }
      } else {
        localStorage.removeItem('favorites');
      }

      this.isFavorite = false;
    },

    getLocalFavorites() {
      if (localStorage.getItem('favorites')) {
        this.favorites = JSON.parse(localStorage.getItem('favorites'));
      }
    },
  },

  mounted() {
    this.getLocalFavorites();
  },
};
</script>

<style lang="scss" scoped>
.photo-wrap {
    position: relative;
    width: 150px;

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

    .photo-text {
        padding-top: 10px;
        display: block;
        letter-spacing: -1px;
    }
}
</style>
