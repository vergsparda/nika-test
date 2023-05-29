<template>
  <div class="album">
    <button class="button album-button" :onClick="handleOpenAlbum">
      <img
        class="icon"
        v-show="isOpen"
        src="../assets/icon-minus.png"
        alt="" width="30" height="30">
      <img
        class="icon"
        v-show="!isOpen"
        src="../assets/icon-plus.png" alt="" width="30" height="30">
      <span class="name">{{ album.title }}</span>
    </button>
    <ul class="photo-list" v-show="isShowPhotos && isOpen">
      <PhotoList :photosList="photosList" />
    </ul>
  </div>
</template>
<script>
import PhotoList from './photoList.vue';

export default {
  name: 'albumItem',
  props: {
    album: {
      type: Object,
      default() {
        return null;
      },
    },
  },

  components: {
    PhotoList,
  },

  data() {
    return {
      isOpen: false,
      photoList: null,
      isShowPhotos: false,
      photosList: null,
    };
  },

  methods: {
    handleOpenAlbum() {
      if (this.isOpen) {
        this.isOpen = !this.isOpen;
      } else {
        const url = `http://jsonplaceholder.typicode.com/photos?albumId=${this.album.id}`;
        this.getPhotoList(url)
          .then((res) => {
            console.log(res);
            this.photosList = res;
            this.isShowPhotos = true;
          });

        this.isOpen = true;
      }
    },

    async getPhotoList(url) {
      try {
        const response = await fetch(url);
        const list = response.json();
        return list;
      } catch (err) {
        console.log(`error ${err}`);
        return null;
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.album {
    .album-button {
        font-size: 18px;
        padding: 20px 5px 20px 130px;
        border-bottom: solid 0.5px #eeeeee;

        &:hover {
        background-color: #dae4ef;
      }
    }

    .icon {
        padding-right: 15px;
    }

    .photo-list {
      flex-direction: row;
      flex-wrap: wrap;
      margin: 0 auto;
      max-width: calc((150px * 3) + (40px * 2));
      gap: 40px;
      padding: 40px 0;
    }
}

</style>
