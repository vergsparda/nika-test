<template>
    <li class="album-item" v-for="album in albums" :key="album.id">
        <AlbumItem :album="album"/>
    </li>
</template>
<script>
import AlbumItem from './albumItem.vue';

export default {
  name: 'AlbumList',
  props: {
    albums: {
      type: Array,
      default() {
        return [];
      },
    },
  },

  components: {
    AlbumItem,
  },

  data() {
    return {};
  },

  methods: {},

  mounted() {},
};
</script>
<style lang="scss">
.album-item {
        width: 100%;
        text-align: left;
}
</style>
