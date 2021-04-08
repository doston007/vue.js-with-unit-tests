<template>
  <li
    class="site-navigation__item"
    :class="{
      'site-navigation__item--has-menu': item.submenu,
      'site-navigation__item--has-menu-open': item.submenu && isSubmenuOpen
    }"
    @click.stop="isSubmenuOpen = !isSubmenuOpen"
  >
    <component
      :is="item.submenu ? 'div' : 'nuxt-link'"
      class="site-navigation__link"
      :to="{ path: link }"
    >
      <img v-if="item.thumbnail" :src="item.thumbnail" :alt="item.name">
      <span>
        {{ item.name }}
      </span>
    </component>
    <menu-list
      v-if="item.submenu"
      v-show="isSubmenuOpen"
      :menu="item.submenu"
      :link="link"
      submenu
    />
  </li>
</template>

<script>
export default {
  name: 'MenuNavItem',
  props: {
    item: {
      type: Object,
      required: true,
    },
    link: {
      type: String,
      default: '',
    },
  },
  data: () => ({
    isSubmenuOpen: false,
  }),
};
</script>

<style lang="scss" scoped>
.site-navigation {
  &__link {
    display: block;
    width: 100%;
    height: 47px;
    position: relative;
    color: #333;
    padding: 0.75rem 1rem;
    display: flex;
    align-items: center;

    img {
      width: 20px;
      height: auto;
      margin-right: 10px;
    }

    &:hover,
    &:active {
      background-color: rgb(130, 0, 255);
      color: rgb(255, 255, 255);
    }
  }

  &__item {
    &--has-menu {
      position: relative;
      &::after {
        content: "";
        position: absolute;
        width: 15px;
        height: 15px;
        right: 15px;
        top: 10px;
        transform: rotate(45deg);
        transition: 0.4s transform;
        border-right: 2px solid #333;
        border-bottom: 2px solid #333;
      }
      &-open::after {
        transform: rotate(45deg) scale(-1);
      }
    }
  }
}
</style>
