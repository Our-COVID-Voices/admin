<template>
  <ul
    class="govuk-list"
    :class="{
      'govuk-list--bullet': bullet,
      'govuk-list--number': number
    }"
  >
    <slot />
  </ul>
</template>

<script>
export default {
  props: {
    bullet: {
      type: Boolean,
      required: false,
      default: false
    },

    number: {
      type: Boolean,
      required: false,
      default: false
    }
  }
}
</script>
