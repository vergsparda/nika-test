<template>
  <div class="person">
    <button class="button person-button" for="person" :onClick="openPerson">
      <img
        class="icon"
        v-show="isOpen"
        src="../assets/icon-minus.png"
        alt="" width="30" height="30">
      <img
        class="icon"
        v-show="!isOpen"
        src="../assets/icon-plus.png" alt="" width="30" height="30">
      <span class="name">{{ person.name }}</span>
    </button>
    <ul class="album-list" v-show="isShowAlbums && isOpen">
      <AlbumList :albums="albums" />
    </ul>
  </div>
</template>

<script>
import AlbumList from './albumList.vue';

export default {
  name: 'personItem',
  props: {
    person: {
      type: Object,
      default() {
        return null;
      },
    },
  },

  components: {
    AlbumList,
  },

  data() {
    return {
      isOpen: false,
      albums: null,
      isShowAlbums: false,
    };
  },

  methods: {
    openPerson() {
      if (this.isOpen) {
        this.isOpen = false;
      } else {
        const url = `http://jsonplaceholder.typicode.com/albums?userId=${this.person.id}`;
        this.getAlbumsList(url)
          .then((res) => {
            this.albums = res;
            this.isShowAlbums = true;
          });

        this.isOpen = true;
      }
    },

    async getAlbumsList(url) {
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
.person {
    .person-button {
        font-size: 22px;
        background-color: unset;
        padding: 20px 5px 20px 70px;
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
