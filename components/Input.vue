<template>
  <div class="gm-input" @click.stop="setFocus($event)" ref="myid"
    :class="{ 'focus': focus, 'empty': empty, 'mandatory': mandatory, 'visited': visited, 'disabled': disabled }, type">
    <label>
      <div class="label-value" for="">{{ label }}</div>
      <div v-if="mandatory && !disabled" class="mandatory-char">*</div>
    </label>
    <input :type="type" :value="value" @focus="focus = true" @focusout="leave"
      @input="$emit('update:value', $event.target.value)" :disabled="disabled" max="2022-12-31">
  </div>
</template>


<script>

export default {
  data() {
    return {
      focus: false,
      visited: false,
    }
  },

  methods: {
    setFocus(e) {
      if (this.disabled || this.focus) {
        return
      }
      this.focus = true
      const input = e.currentTarget.querySelector('input');

      input.focus();

    },

    leave() {
      if (this.focus) {
        this.visited = true
      }
      this.focus = false
    }
  },

  computed: {
    empty() {
      return this.value === ''
    }
  },
  props: {
    label: String,
    value: String,
    type: {
      type: String,
      default: 'text'
    },
    mandatory: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
$gm-color-black: #00101A;
$gm-color-main: #0025A4;
$gm-color-red: #F35B5B;

.gm-input {
  cursor: text;

  box-sizing: border-box;
  position: relative;

  height: 48px;
  padding: 9px 12px;

  background: #FFFFFF;
  box-shadow: 0 0 0 1px rgba($gm-color-black, 0.04);
  border-radius: 6px;

  font-family: 'Inter',
    sans-serif;
  font-size: 13px;
  letter-spacing: -0.0025em;

  transition: outline 120ms ease-out;

  &.disabled {
    opacity: 0.6;
  }


  input {
    position: absolute;
    top: 23px;
    left: 12px;

    padding: 0;
    outline: none;
    border: none;


    color: #00101A;
    background: transparent;

    font-size: inherit;
    letter-spacing: inherit;

    &::placeholder {
      color: rgba($gm-color-black, 0.2);
    }
  }

  label {
    position: absolute;
    top: 16px;
    left: 12px;

    display: flex;
    flex-flow: row;

    transition: 60ms ease-out;

    .label-value {
      color: rgba($gm-color-black, 0.5);
    }

    .mandatory-char {
      color: $gm-color-red;
    }
  }

  &:hover:not(.focus, .disabled) {
    box-shadow: 0 0 0 1px rgba($gm-color-black, 0.2);
  }

  &.focus,
  &.week,
  &.date,
  &:not(.empty) {

    label {
      top: 9px;

      font-size: 11px;
      line-height: 13px;
      letter-spacing: -0.004em;
    }

    input {
      visibility: visible;
    }
  }

  &.focus {
    box-shadow: 0 0 0 1px rgba($gm-color-main, 0.7);
  }

  &.mandatory.empty.visited {
    box-shadow: 0 0 0 1px rgba($gm-color-red, 0.7);
  }
}
</style>