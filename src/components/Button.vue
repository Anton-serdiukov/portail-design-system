<!--
  Button with an optional icon and different styles

  Usage:

    <Button
      :big="true"             - Big button
      :alt="boolean"          - Alt button
      :plain="boolean"        - Plain button
      :icon="account_circle"  - Left icon
      :icon-right="edit    "  - Right icon
    >
      Button label
    </Button>
-->

<template>
  <button :class="['button', {primary, big, alt, plain}]">
    <Icon
      v-if="icon"
      :class="{'icon-left': hasLabel}"
      :source="icon"
      :size="big ? '28px' : '24px'"
      :color="primary ? 'white' : alt ? 'brand' : 'black'"
    />
    <slot></slot>
    <Icon
      class="icon-right"
      v-if="iconRight"
      :source="iconRight"
      :size="big ? '28px' : '24px'"
      :color="primary ? 'white' : alt ? 'brand' : 'black'"
    />
  </button>
</template>

<script>
import Icon from './Icon.vue'

export default {
  name: 'Button',
  components: {Icon},
  props: {
    big: Boolean,
    alt: Boolean,
    plain: Boolean,
    icon: String,
    iconRight: String,
  },
  data: () => ({
  }),
  computed: {
    primary() {
      return !(this.alt || this.plain)
    },
    hasLabel() {
      return !!this.$slots.default
    },
  }
}
</script>

<style lang="less">
@import '../styles/vars';

.button {
  -moz-appearance: none;
  -webkit-appearance: none;
  background: none;
  border-radius: 3px;
  border: none;
  box-sizing: border-box;
  cursor: pointer;
  display: inline-block;
  margin: 0;
  transition: background 250ms ease-in-out;

  padding: 10px 16px;
  &.big {
    padding: 14px 24px;
  }

  .icon {
    margin: -4px;
  }
  .icon-left {
    margin-left: -10px;
    margin-right: 5px;
  }
  .icon-right {
    margin-right: -10px;
    margin-left: 5px;
  }

  &.primary {
    .font-button-normal();
    background: @color-brand;

    &.big {
      .font-button-big();
    }

    &:hover, &:focus {
      background: darken(@color-brand, 5%);
    }

    &:active {
      background: darken(@color-brand, 10%);
    }
  }

  &.alt {
    .font-button-normal-alt();
    background: @color-white;
    border: 1px solid @color-brand;
  }

  &.alt, &.plain {
    &:hover, &:focus {
      background: darken(@color-white, 5%);
    }

    &:active {
      background: darken(@color-white, 10%);
    }
  }

  &:focus {
    outline: 1px dashed @color-gray-400;
    outline-offset: -2px;
  }
}
</style>