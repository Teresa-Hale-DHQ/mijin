<template>
  <component
    :is="props.tag"
    :ref="data.ref"
    class="flex border-b border-gray-300 dark:border-gray-600 space-x-4"
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
    <slot />
  </component>
</template>

<script>
export default {
  name: 'MijinTabs',

  props: {
    tag: {
      default: 'ul',
      type: String,
    },
  },
};
</script>
