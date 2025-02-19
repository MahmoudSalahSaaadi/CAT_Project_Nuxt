<script setup>
import BaseToast from '~/components/_Shared/BaseToast.vue';
</script>

<template>
  <div>
    <SharedHomeBaseHeader />
    <main class="relative flex h-screen">
      <div class="w-full  h-full">

        <slot />
      </div>
    </main>
    <BaseToast />
  </div>
</template>
