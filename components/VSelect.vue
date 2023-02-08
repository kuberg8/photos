<template>
  <div
    v-on-clickaway="close"
    class="input select"
    :class="{ error: touched && !inputValue, open: isOpen }"
    @click="toggle"
  >
    <div>
      <div v-if="!!inputValue" class="elipsis">
        {{ inputValue }}
      </div>

      <div v-else class="placeholder">
        {{ placeholder }}
      </div>
    </div>

    <div v-if="isOpen" class="menu">
      <div
        v-for="(item, i) in options"
        :key="i"
        class="item"
        :class="{ selected: item === inputValue }"
        @click="inputValue = item"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: '',
    },
    options: {
      type: Array,
      default: () => [],
    },
    placeholder: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      isOpen: false,
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
  methods: {
    toggle() {
      this.isOpen = !this.isOpen
    },
    close() {
      if (this.isOpen) {
        this.isOpen = false
        this.touched = true
      }
    },
    clear() {
      this.inputValue = null
      this.close()
    },
  },
}
</script>

<style lang="scss" scoped>
.select {
  position: relative;
  cursor: pointer;

  &.open {
    border-bottom: none;
  }

  &.error {
    .menu {
      border-color: red;
    }
  }

  .elipsis {
    display: inline;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
    max-width: inherit;
  }

  .menu {
    position: absolute;
    top: 100%;
    left: -1px;
    border: 1px solid #c7c7c7;
    border-top: none;
    width: calc(100% + 2px);
    background: white;
    z-index: 10;

    .item {
      padding: 6px 20px;
      transition: opacity 0.5s;

      &:hover,
      &.selected {
        opacity: 0.5;
      }
    }
  }
}
</style>
