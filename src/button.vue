<template>
    <button class="g-button" :class="{[`icon-${iconPosition}`]: true}"
      @click="$emit('click')">
      <y-icon :name="icon" v-if="icon && !loading" class="icon"></y-icon>
      <y-icon class="loading icon" name="loading" v-if="loading"></y-icon>
      <div class="content">
        <slot></slot>
      </div>
    </button>
</template>
<script>
  export default  {
    props: {
      icon: {},
      loading: {
        type: Boolean,
        default: false
      },
      iconPosition: {
        type: String,
        default: 'left',
        validator (position) {
          return !(position !== 'left' && position !== 'right')
        }
      }
    },
    methods: {
    }
  }
</script>
<style lang="scss">
  .g-button {
    @keyframes spin {
      0% { transform: rotate(0deg) }
      100% { transform: rotate(360deg) }
    }
    font-size: var(--font-size); height: var(--button-height); padding: 0 1em;
    background: var(--button-bg);
    border-radius: var(--border-radius); border: 1px solid var(--border-color);
    display: inline-flex; justify-content: center; align-items: center;
    vertical-align: middle;
    &:hover { border-color: var(--border-color-hover); }
    &:active { background-color: var(--button-active-bg); }
    &:focus { outline: none; }
    > .content { order: 2; }
    > .icon { order: 1; margin-left: 0; margin-right: .3em; }

    &.icon-right {
      > .content { order: 1; }
      > .icon { order: 2; margin-left: .3em; margin-right: 0; }
    }
    .loading {
      animation: spin 1.3s infinite linear;
    }
  }
</style>