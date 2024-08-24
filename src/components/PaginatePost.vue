<script setup>
defineProps(["inicio", "fin", "maxLength"])
const emit = defineEmits(["next", "previus"]);
</script>

<template>
  <div class="btn-group" role="group" aria-label="Basic outlined example">
    <button
      type="button"
      class="btn btn-outline-primary"
      @click="emit('previus')"
      :disabled="inicio==0"
    >
      Previus
    </button>
    <button type="button" class="btn btn-outline-primary" @click="emit('next')" :disabled="fin == maxLength">
      Next
    </button>
  </div>
</template>
