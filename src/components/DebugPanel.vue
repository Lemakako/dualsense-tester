<script setup lang="ts">
import { useDualSenseStore } from '@/store/dualsense'
import { storeToRefs } from 'pinia'
import { computed } from 'vue'
import GeneralContainer from './common/GeneralContainer.vue'

const { inputReport } = storeToRefs(useDualSenseStore())
// inputReport is a ref of dataview
const stringifyReport = computed(() => {
  if (!inputReport.value)
    return ''
  const dv = inputReport.value
  const arr = new Uint8Array(dv.buffer)
  return arr.reduce((acc, val) => `${acc + val.toString(16).padStart(2, '0')} `, '')
})
</script>

<template>
  <GeneralContainer title="Debug" tag="dev-only">
    <textarea
      :value="stringifyReport" readonly
      class="block h-10em w-full resize-none rounded-2xl bg-transparent p-1 font-mono dou-sc-autoborder"
    />
  </GeneralContainer>
</template>

<style scoped></style>
