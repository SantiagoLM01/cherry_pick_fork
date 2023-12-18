<script setup lang="ts">
const props = defineProps({
  header: {
    type: String,
    required: true,
    default: "",
  },
  field: {
    type: String,
    required: true,
    default: "",
  },
  value: { type: Object },
});

</script>

<template>
  <td
    class="text-[#687684] text-center min-w-[174px] px-4 "
  >

    <slot v-if="value.value">
      {{ value.value[field] }}
    </slot>
  </td>
</template>
