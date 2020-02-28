<template>
  <div
    v-ripple
    :class="backgroundColor"
    class="button flex flex-center relative-position"
    @click="onClick"
  >
    {{ label }}
  </div>
</template>

<script>
export default {
  props: ['label', 'bgColor'],

  methods: {
    onClick(event) {
      this.$emit('onClick', event)
    }
  },

  computed: {
    backgroundColor() {
      return `bg-${this.bgColor || 'primary'}`
    }
  }
}
</script>

<style scoped lang="scss">
.button {
  border-radius: 2px;
  padding: 10px 15px;
  color: white;
  font-weight: bold;
  cursor: pointer;
}
</style>
