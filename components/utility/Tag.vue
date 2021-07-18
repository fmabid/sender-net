<template>
  <div>
    <span class="py-0.5 px-2 rounded-full bg-gray-300 text-xs text-gray-600">
      {{ tagName }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    tagName: {
      default: '',
      type: String,
      required: true,
    },
  },
}
</script>

<style></style>
