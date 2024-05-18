<template lang="html">
  <div class='tab-content' v-show='title == selectedTitle'>
    <slot></slot>
  </div>
</template>

<script lang="ts">
import { inject } from 'vue'

export default {
  props: ['title'],
  setup() {
    const selectedTitle = inject("selectedTitle")

    return {
      selectedTitle
    }
  }
}
</script>

<style scoped lang="css">
.flex {
  display: flex;
  gap: 1.5em;
	justify-content: space-evenly;
}
.flex:has(.pie-chart) {
  flex-wrap: wrap;
}
.tab-content {
  padding-top: 1.5em;
}
</style>
