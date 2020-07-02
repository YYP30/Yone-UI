<template>
    <button class="g-button" :class="{[`icon-${iconPosition}`]: true}">
      <y-icon :name="icon" v-if="icon"></y-icon>
      <div class="content">
        <slot></slot>
      </div>
    </button>
</template>
<script>
  export default  {
    // props: ['icon', 'iconPosition']
    props: {
      icon: {},
      iconPosition: {
        type: String,
        default: 'left',
        validator (position) {
          return !(position !== 'left' && position !== 'right')
        }
      }

    }
  }
</script>
<style lang="scss">
  .g-button {
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
  }
</style>