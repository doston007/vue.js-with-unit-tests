<template>
  <nav class="site-nav" :class="{ 'site-nav--show': menu_is_visible }">
    <menu-list :menu="menu" link="catalog" />
  </nav>
</template>

<script>
import { mapState } from 'vuex';

import MenuList from '~/components/menu/MenuList.vue';

export default {
  components: { MenuList },
  computed: {
    ...mapState({
      menu: (state) => state.the_menu.menu,
      menu_is_visible: (state) => state.the_menu.menu_is_visible,
    }),
  },
};
</script>

<style lang="scss" scoped>
.site-nav {
  height: 0;
  opacity: 0;
  visibility: hidden;
  pointer-events: none;
  overflow-y: auto;
  background: #fff;
  transition: .4s all;

  &--show {
    height: 100vh;
    opacity: 1;
    pointer-events: auto;
    visibility: visible;
  }
}
</style>
