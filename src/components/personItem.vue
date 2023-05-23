<template>
    <div class="person">
        <button class="person-checkbox" for="person" :onClick="openPerson">
            <img
                class="icon" v-show="isOpen"
                src="../assets/icon-minus.png"
                alt="" width="30" height="30">
            <img
                class="icon" v-show="!isOpen"
                src="../assets/icon-plus.svg"
                alt="" width="30" height="30">
            <span class="name">{{ person.name }}</span>
        </button>
    </div>
</template>

<script>
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

  data() {
    return {
      isOpen: false,
    };
  },

  methods: {
    openPerson() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>
<style lang="scss">
.person {
    cursor: pointer;
    padding: 20px 5px 20px 70px;
    border-bottom: solid 0.5px #eeeeee;

    .person-checkbox {
        display: flex;
        font-size: 22px;
        width: 100%;
        cursor: pointer;
        border: none;
        text-align: left;
        background-color: unset;
        align-items: center;
    }

    &:hover {
        background-color: #dae4ef;
    }

    .input {
        display: none;
    }

    .icon {
        padding-right: 15px;
    }
}
</style>
