<template functional>
  <div
    :class="[data.class, data.staticClass, 'sf-quantity-selector']"
    :style="[data.style, data.staticStyle]"
  >
    <component
      :is="injections.components.AwButton"
      :disabled="
        props.disabled || Boolean(props.min !== null && props.qty <= props.min)
      "
      class="sf-button--pure sf-quantity-selector__button"
      data-testid="decrease"
      @click="
        $options.handleInput(
          Number(props.qty) - 1,
          listeners,
          props.min,
          props.max
        )
      "
    >
      &minus;
    </component>
    <component
      :is="injections.components.SfInput"
      type="number"
      :name="$options.uniqueKey()"
      :value="Number(props.qty)"
      :disabled="props.disabled"
      class="sf-quantity-selector__input"
      data-testid="sf-quantity-selector input"
      @input="$options.handleInput($event, listeners, props.min, props.max)"
      @blur="$options.handleBlur(listeners)"
    />
    <component
      :is="injections.components.AwButton"
      :disabled="
        props.disabled || Boolean(props.max !== null && props.qty >= props.max)
      "
      class="sf-button--pure sf-quantity-selector__button"
      data-testid="increase"
      @click="
        $options.handleInput(
          Number(props.qty) + 1,
          listeners,
          props.min,
          props.max
        )
      "
    >
      +
    </component>
  </div>
</template>
<script>
import AwButton from '../atoms/AwButton.vue';
import {
  SfInput,
} from "@storefront-ui/vue";

export default {
  name: "SfQuantitySelector",
  inject: {
    components: {
      default: {
        SfInput,
        AwButton,
      },
    },
  },
  model: {
    prop: "qty",
  },
  props: {
    qty: {
      type: [Number, String],
      default: 1,
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    min: {
      type: Number,
      default: null,
    },
    max: {
      type: Number,
      default: null,
    },
  },
  handleInput(qty, listeners, min, max) {
    // adjust qty per min/max if needed
    const minimum = min || 1;
    if (qty < minimum || isNaN(qty)) {
      qty = minimum;
    } else if (max !== null && qty > max) {
      qty = max;
    }
    return listeners.input && listeners.input(qty);
  },
  handleBlur(listeners) {
    return listeners.blur && listeners.blur();
  },
  uniqueKey() {
    const key = Math.random().toString(16).slice(2);
    return "quantitySelector" + key;
  },
};
</script>
