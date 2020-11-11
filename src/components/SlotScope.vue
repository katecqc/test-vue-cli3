<template>
  <span>
    <slot v-bind:user="user">
      {{ user.lastName }}
    </slot>
  </span>
</template>

<script>
export default {
  name: 'SlotScope',
  props: {
    user: {
      type: Object,
      default: () => {
        return {
          firstName: 'Kate',
          lastName: 'Chan'
        }
      }
    }
  }
}
</script>

<style scoped>

</style>
