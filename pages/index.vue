<template>
  <slot />
</template>

<script setup lang="ts">
const router = useRouter()
onBeforeMount(() => {
  router.push({ path: `/profile/1`})
})
</script>
