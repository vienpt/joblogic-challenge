<template>
  <div class="main">
    <Nav></Nav>

    <main>
      <TheHeader></TheHeader>

      <div class="pl-80 bg-gray-700 h-[100vh]">
        <slot></slot>
      </div>
    </main>
  </div>
</template>

<script setup lang="ts"></script>
<style lang="postcss">
.main {
  @apply flex flex-col mx-auto overflow-hidden h-[100vh];
}
</style>
