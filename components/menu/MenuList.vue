<template>
  <ul class="site-navigation" :class="{ 'site-navigation--submenu': submenu }">
    <menu-nav-item
      v-for="item in menu"
      :key="item.id"
      :item="item"
      :link="`${link}/${item.slug}`"
    />
  </ul>
</template>

<script>
export default {
  name: 'MenuList',
  props: {
    menu: {
      type: Array,
      required: true,
    },
    submenu: {
      type: Boolean,
      default: false,
    },
    link: {
      type: String,
      default: '/',
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~assets/variables";

.site-navigation {
  display: flex;
  flex-direction: column;
  grid-area: site-navigation;
  list-style-type: none;
  width: 100%;
  background: rgb(255, 255, 255);
  z-index: 1;
  padding-left: 0;

  &--submenu {
    padding-left: 15px;
    position: relative;
    animation: slideIn 0.4s ease-in;
    &::before {
      content: "";
      position: absolute;
      bottom: 0;
      top: 0;
      border-left: 1px solid #000;
      left: 7.5px;
    }
  }

  &__grid {
    display: grid;
    grid-template-rows: 90px 90px;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    list-style-type: none;
    padding: 0;
  }

  &__grid-item {
    display: flex;
    align-items: center;
    position: relative;
    height: 100%;
    text-align: center;
    color: rgb(130, 0, 255);
    border-right: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
  }

  &__link {
    display: block;
    width: 100%;
    color: inherit;

    &:hover,
    &:active {
      color: rgb(255, 255, 255);
    }

    &--special {
      display: flex;
      align-items: center;
      position: absolute;
      padding-left: 50%;
      left: -10%;
      height: 100%;

      &:hover,
      &:active {
        color: inherit;
      }
    }
  }
}

@keyframes slideIn {
  from {
    max-height: 0;
    opacity: 0;
  }
  to {
    max-height: 5000px;
    opacity: 1;
  }
}
</style>
