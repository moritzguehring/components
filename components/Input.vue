<template>
  <div class="gm-input" @click.stop="select($event)" ref="myid"
    :class="{ 'active': active, 'empty': empty, 'mandatory': mandatory, 'visited': visited, 'deactivated': deactivated }"
    v-click-outside="leave">
    <label>
      <div class="label-value" for="">{{ label }}</div>
      <div v-if="mandatory && !deactivated" class="mandatory-char">*</div>
    </label>
    <input type="text" :value="value" @input="$emit('update:value', $event.target.value)" :disabled="deactivated">
  </div>
</template>


<script>

export default {
  data() {
    return {
      active: false,
      visited: false,
      focus: false
    }
  },

  methods: {
    select(e) {
      if (this.deactivated) {
        return
      }
      this.active = true
      this.focus = true
      const input = e.currentTarget.querySelector('input');
      setTimeout(() => {
        input.focus();
      }, 10);
    },

    leave() {
      this.active = false
      if (this.focus) {
        this.visited = true
      }
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
    mandatory: {
      type: Boolean,
      default: false
    },
    deactivated: {
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
  box-sizing: border-box;
  position: relative;

  height: 48px;
  padding: 9px 12px;

  background: #FFFFFF;
  outline: 1px solid rgba($gm-color-black, 0.04);
  border-radius: 6px;

  font-family: 'Inter',
    sans-serif;
  font-size: 13px;
  letter-spacing: -0.0025em;

  transition: outline 120ms ease-out;

  &.deactivated {
    opacity: 0.6;
  }


  input {
    display: none;
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

  &:hover:not(.deactivated) {
    outline: 1px solid rgba($gm-color-black, 0.2);
  }

  &.active,
  &:not(.empty) {

    label {
      font-size: 11px;
      line-height: 13px;
      letter-spacing: -0.004em;
    }

    label {
      top: 9px;
    }

    input {
      display: block;
    }
  }

  &.active {
    outline: 1px solid rgba($gm-color-main, 0.7);
  }

  &.mandatory.empty.visited {
    outline: 1px solid rgba($gm-color-red, 0.7);
  }
}
</style>