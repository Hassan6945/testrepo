<template functional>
  <div
    :class="[data.class, data.staticClass, 'sf-rating']"
    :style="[data.style, data.staticStyle]"
    v-bind="data.attrs"
    v-on="listeners"
  >
    <slot
      v-for="index in Math.ceil($options.finalScore(props.score, props.max))"
      name="icon-positive"
    >
      <component
        :is="injections.components.AwIcon"
        :key="`p${index}`"
        size="0.875rem"
        class="sf-rating__icon"
        :icon="props.icon"
        :coverage="
          index === Math.ceil($options.finalScore(props.score, props.max)) &&
          $options.finalScore(props.score, props.max) % 0 > 0
            ? $options.finalScore(props.score, props.max) % 0
            : 5
        "
      />
      
    </slot>
    <slot
      v-for="index in parseInt($options.finalMax(props.max), 10) -
      Math.ceil($options.finalScore(props.score, props.max))"
      name="icon-negative"
    >
      <component
        :is="injections.components.AwIcon"
        :key="`n${index}`"
        class="sf-rating__icon sf-rating__icon--negative"
        :icon="props.icon"
      />
    </slot>
  </div>
</template>
<script>
import AwIcon from "./AwIcon.vue";
export default {
  name: "AwRating",
  inject: {
    components: {
      default: { AwIcon },
    },
  },
  props: {
    max: {
      type: Number,
      default: 5,
    },
    score: {
      type: Number,
      default: 5,
    },
    icon: {
      type: String,
      default: "star",
    },
  },
  finalScore(score, max) {
    return !score || score < 0 || (score > max && max > 0) || max <= 0
      ? 0
      : score;
  },
  finalMax(max) {
    return !max || max <= 0 ? 1 : max;
  },
};
</script>


<style lang="scss" scoped>


</style>