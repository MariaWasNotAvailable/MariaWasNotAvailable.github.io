<template lang="html">
  <div class="tabs">
    <ul class="tabs-header">
      <div v-for="title in tabTitles" 
        :key="title"
        :class="{ active: selectedTitle == title }"
        @click = "selectedTitle = title"
      >
        <li>
          {{ title }}
        </li>
      </div>
    </ul>
    <slot />
  </div>
</template>

<script lang="ts">
import { ref, provide } from 'vue'
import { defineComponent } from 'vue'

export default defineComponent({
  setup (props, { slots }) {
    const tabTitles = ref(slots.default!().map((tab) => tab.props!.title))
    const selectedTitle = ref(tabTitles.value[0])

    provide ("selectedTitle", selectedTitle)
    return {
      selectedTitle,
      tabTitles
    }
  }
})
</script>

<style scoped lang="css">
.tabs-header > li {
  color: #00102A !important;
}
.active {
  border-style: solid none none;
  border-color: #003E80;
  background-color: white;
}
.tabs-header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding-left: 0;
  background-color: #EFEFEF;
}
.tabs-header > div {
  cursor: pointer;
  width: 100%;
  line-height: 2.5em;
  display: block;
  box-sizing: inherit;
  text-align: center;
  list-style: none;
}
.tabs-header > div:hover:not(.active) {
  transition: ease-in-out 0.2s;
  background-color: #F3F3F3;
}
</style>