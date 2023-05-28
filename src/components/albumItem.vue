<template>
  <div class="album">
    <button class="button album-button" :onClick="openAlbum">
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
    <!-- <ul class="album-list" v-show="isShowAlbums">
      <AlbumList :albums="albums" />
    </ul> -->
  </div>
</template>
<script>
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
  },

  data() {
    return {
      isOpen: false,
      albums: null,
    };
  },

  methods: {
    openAlbum() {
      this.isOpen = !this.isOpen;
    },

    // async getAlbumsList(url) {
    //   try {
    //     const response = await fetch(url);
    //     const list = response.json();
    //     return list;
    //   } catch (err) {
    //     console.log(`error ${err}`);
    //     return null;
    //   }
    // },
  },

  mounted() {
    // const url = `http://jsonplaceholder.typicode.com/albums?userId=${this.person.id}`;
    // this.getAlbumsList(url)
    //   .then((res) => {
    //     this.albums = res;
    //     this.isShowAlbums = true;
    //   });
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
}

</style>
