<template>
  <component
    :is="props.tag"
    :ref="data.ref"
    class="inline-block relative h-3 w-3"
    :class="[
      data.class,
      data.staticClass,
    ]"
    :style="[
      data.style,
      data.staticStyle,
    ]"
    v-bind="data.attrs"
    v-on="listeners"
  >
    <div
      v-if="props.animate"
      class="animate-ping absolute h-full w-full rounded-full opacity-75"
      :class="[
        {
          'bg-danger-500': ['danger', 'error'].includes(props.status),
          'bg-gray-500': props.status === 'disabled',
          'bg-primary-500': props.status === 'primary',
          'bg-success-500': props.status === 'success',
          'bg-warning-500': props.status === 'warning',
        },
      ]"
    />

    <div
      class="absolute rounded-full h-full w-full"
      :class="[
        {
          'bg-danger-500': ['danger', 'error'].includes(props.status),
          'bg-gray-500': props.status === 'disabled',
          'bg-primary-500': props.status === 'primary',
          'bg-success-500': props.status === 'success',
          'bg-warning-500': props.status === 'warning',
        },
      ]"
    />
  </component>
</template>

<script>
const validator = {
  status: [
    'danger',
    'disabled',
    'primary',
    'success',
    'warning',
  ],
};

export default {
  name: 'MijinStatusDot',

  validator,

  props: {
    animate: {
      default: false,
      type: Boolean,
    },

    status: {
      default: 'primary',
      type: String,
      validator: (value) => validator.status.includes(value),
    },

    tag: {
      default: 'div',
      type: String,
    },
  },
};
</script>
