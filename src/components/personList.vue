<template>
    <div class="list-item" v-for="person in list" :key="person.id">
        <PersonItem :person="person"/>
    </div>
  </template>

<script>
import PersonItem from './personItem.vue';

export default {
  name: 'PersonList',
  props: {
    list: {
      type: Array,
      default() {
        return [];
      },
    },
  },

  components: {
    PersonItem,
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

    .list-item {
        width: 100%;
        text-align: left;
    }
}
</style>
