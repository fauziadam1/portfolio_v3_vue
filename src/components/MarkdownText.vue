<script setup>
defineProps({
  text: {
    type: String,
    required: true,
  },
});

const renderMarkdown = (value) =>
  value.replace(
    /\[([^\]]+)\]\((https?:\/\/[^)]+)\)/g,
    '<a href="$2" target="_blank" rel="noopener noreferrer">$1</a>',
  );
</script>

<template>
  <span v-html="renderMarkdown(text)" />
</template>
