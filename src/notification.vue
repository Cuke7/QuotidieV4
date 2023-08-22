<template>
  <div>
    <label class="swap swap-rotate">
      <input type="checkbox" />
      <BellAlertIcon class="h-6 w-6 text-red-800 swap-on" />
      <BellSlashIcon class="h-6 w-6 text-red-800 swap-off" />
    </label>
  </div>
</template>

<script lang="ts" setup>
import { BellAlertIcon, BellSlashIcon } from "@heroicons/vue/24/solid";
</script>
