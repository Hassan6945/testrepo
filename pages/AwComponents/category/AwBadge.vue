<template functional>
  <span
    :class="[data.class, data.staticClass, 'sf-badge']"
    :style="[data.style, data.staticStyle]"
    v-bind="data.attrs"
    v-on="listeners"
  >
    <slot />
  </span>
</template>
<script>
export default {
  name: "AwBadge",
};
</script>
