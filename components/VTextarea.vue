<template>
  <textarea
    v-model.trim="inputValue"
    v-mask="mask"
    type="text"
    class="input"
    @blur="touched = true"
    rows="4"
    :class="{ error: touched && !inputValue }"
  />
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: null,
    },
    mask: {
      type: String,
      default: null,
    },
  },
  data() {
    return {
      touched: false,
    }
  },
  computed: {
    inputValue: {
      get() {
        return this.value
      },
      set(value) {
        this.$emit('input', value)
      },
    },
  },
}
</script>
