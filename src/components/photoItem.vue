<template>
    <div class="photo">
        <img
          class="photo-img"
          :src="photo.thumbnailUrl" :alt="photo.title">
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
    handleOpenPhoto() {
    },
  },
};
</script>
  <style lang="scss" scoped>
  .photo {
    height: 150px;
    width: 150px;
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
