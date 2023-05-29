<template>
    <li class="photo-item" v-for="photo in photosList" :key="photo.id">
        <PhotoItem :photo="photo"/>
    </li>
</template>
<script>
import PhotoItem from './photoItem.vue';

export default {
  name: 'AlbumList',
  props: {
    photosList: {
      type: Array,
      default() {
        return [];
      },
    },
  },

  components: {
    PhotoItem,
  },

  data() {
    return {};
  },

  methods: {},

  mounted() {},
};
</script>
<style lang="scss">
.list {
    display: flex;
    flex-direction: column;
    align-items: flex-start;

    .album-item {
        width: 100%;
        text-align: left;
    }
}
</style>
