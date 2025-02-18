<template>
  <component
    :is="props.tag"
    :ref="data.ref"
    :class="[
      'relative leading-tight font-button border transition-colors duration-150 focus:outline-none shadow-sm',
      {
        // busy
        'animate-pulse': props.busy,
        // variant
        'text-white border-primary-500 bg-primary-500 hover:border-primary-600 hover:bg-primary-600 focus:bg-primary-600 active:bg-primary-700':
          props.variant === 'primary' && props.color === 'primary' && !props.disabled,
        'text-white border-danger-500 bg-danger-500 hover:border-danger-600 hover:bg-danger-600 focus:bg-danger-600 active:bg-danger-700':
          props.variant === 'primary' && props.color === 'danger' && !props.disabled,
        'text-white border-warning-500 bg-warning-500 hover:border-warning-600 hover:bg-warning-600 focus:bg-warning-600 active:bg-warning-700':
          props.variant === 'primary' && props.color === 'warning' && !props.disabled,
        'text-white border-success-500 bg-success-500 hover:border-success-600 hover:bg-success-600 focus:bg-success-600 active:bg-success-700':
          props.variant === 'primary' && props.color === 'success' && !props.disabled,
        'border-gray-300 dark:border-gray-600 hover:border-gray-400 dark:hover:border-gray-500 active:border-gray-500 dark:active:border-gray-300':
          props.variant === 'secondary' && !props.disabled,
        // disabled
        'border-gray-300 dark:border-gray-600 bg-gray-200 dark:bg-gray-700 text-gray-600 dark:text-gray-400 cursor-not-allowed': props.disabled,
        // loading
        'cursor-wait': props.loading || props.busy,
        'cursor-pointer ': !props.loading || !props.busy,
        // icon
        'inline-flex items-center': $slots.icon || props.icon,
        'flex-row-reverse': props.iconRight,
        // size
        'px-4 py-1': $slots.default && props.size === 'sm',
        'px-5 py-2': $slots.default && props.size === 'base',
        'px-10 py-4': $slots.default && props.size === 'lg',
        'px-3 py-2': !$slots.default,
        // group
        'rounded-button': props.group === false,
        'rounded-l-button': props.group === 'first',
        'rounded-r-button': props.group === 'last',
      },
      data.class,
      data.staticClass,
    ]"
    :style="[
      data.style,
      data.staticStyle,
    ]"
    :aria-busy="props.loading ? 'true' : null"
    :aria-disabled="props.tag !== 'button' && props.disabled ? 'true' : null"
    :disabled="props.disabled || props.loading"
    :type="props.tag === 'button' ? props.type : null"
    v-bind="data.attrs"
    v-on="listeners"
  >
    <div
      v-if="props.loading"
      class="absolute inset-0 flex items-center justify-center w-full"
    >
      &#8203;
      <div class="rounded-full h-2 w-2 mx-1 bg-current animate-pulse" />
      <div class="rounded-full h-2 w-2 mx-1 bg-current animate-pulse animation-delay-300" />
      <div class="rounded-full h-2 w-2 mx-1 bg-current animate-pulse animation-delay-600" />
      &#8203;
    </div>

    <span
      v-if="$slots.icon"
      class=""
      :class="[
        'w-4 h-4 inline-flex items-center',
        {
          'opacity-0': props.loading,
          'mr-1': $slots.default && !props.iconRight,
          'ml-1': $slots.default && props.iconRight,
        }
      ]"
    >
      <slot name="icon" />
    </span>
    <span :class="{ 'opacity-0': props.loading }">
      <slot />
    </span>
    <span v-if="!$slots.default">&#8203;</span>
  </component>
</template>

<script>
const validator = {
  color: [
    'danger',
    'primary',
    'warning',
  ],
  group: [
    false,
    true,
    '',
    'first',
    'last',
  ],
  size: [
    'sm',
    'base',
    'lg',
  ],
  variant: [
    'primary',
    'secondary',
  ],
};

export default {
  name: 'MijinButton',

  validator,

  props: {
    busy: {
      default: false,
      type: Boolean,
    },

    color: {
      default: 'primary',
      type: String,
      validator: (value) => validator.color.includes(value),
    },

    disabled: {
      default: false,
      type: Boolean,
    },

    group: {
      default: false,
      type: [String, Boolean],
      validator: (value) => validator.group.includes(value),
    },

    icon: {
      default: null,
      type: String,
    },

    iconRight: {
      default: false,
      type: Boolean,
    },

    loading: {
      default: false,
      type: Boolean,
    },

    size: {
      default: 'base',
      type: String,
      validator: (value) => validator.size.includes(value),
    },

    tag: {
      default: 'button',
      type: String,
    },

    type: {
      type: String,
      default: 'button',
    },

    variant: {
      default: 'primary',
      type: String,
      validator: (value) => validator.variant.includes(value),
    },
  },
};
</script>
