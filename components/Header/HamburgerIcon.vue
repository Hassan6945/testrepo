<template>
  <button
    type="button"
    class="bg-cl-transparent brdr-none inline-flex"
    @click="toggleSidebar"
    :aria-label="$t('Open menu')"
    data-testid="menuButton"
  >
    <i class="material-icons">dehaze</i>
  </button>
</template>

<script>
import HamburgerIcon from '@vue-storefront/core/compatibility/components/blocks/Header/HamburgerIcon'

export default {
  mixins: [HamburgerIcon],
  methods: {
    toggleSidebar () {
      this.$emit('toggleSidebar');
      console.log("in func");
    }
  }
}
</script>
