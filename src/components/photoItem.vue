<template>
    <button class="photo" @click="handlePhotoButton">
        <img
          class="photo-img"
          :src="photo.thumbnailUrl" :alt="photo.title">
    </button>
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

  components: {
  },

  data() {
    return {
      isOpen: false,
      photoList: null,
      isShowPhotos: false,
    };
  },

  methods: {
    handlePhotoButton() {
      const popup = document.querySelector('.popup');
      const image = document.createElement('img');
      const popupImage = document.querySelector('.popup-image');

      if (popupImage) {
        popup.removeChild(popupImage);
      }

      popup.classList.add('active');

      image.src = this.photo.url;
      image.alt = this.photo.title;
      image.classList.add('popup-image');
      image.style.borderRadius = '5px';

      popup.insertAdjacentElement('afterbegin', image);

      console.log(popup);
    },
  },
};
</script>
  <style lang="scss" scoped>
  .photo {
    height: 150px;
    width: 150px;
    padding: 0;
      .photo-button {

          &:hover {
          background-color: #dae4ef;
        }
      }

      .photo-img {
        border-radius: 5px;
      }
  }

  </style>
