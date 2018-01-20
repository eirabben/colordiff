<template>
  <input class="color-input" ref="input" type="text" placeholder="#ffffff" v-bind:value="value" v-on:input="updateValue($event.target.value)">
</template>

<script>
export default {
  name: 'color-input',
  props: ['value'],
  methods: {
    updateValue: function(value) {
      if (this.validateHex(value)) {
        // this.$refs.input.value = value
        this.$emit('input', value)
      }
    },

    validateHex: function(value) {
      if (/(^[0-9A-F]{6}$)|(^[0-9A-F]{3}$)/i.test(value)) {
        
      } else if (/(^#[0-9A-F]{6}$)|(^#[0-9A-F]{3}$)/i.test(value)) {
        return true
      }
      return false
    }
  }
}
</script>
