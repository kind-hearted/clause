<script setup>
import { onMounted, ref } from 'vue'
import Pdf from '@/components/Pdf.vue'

const show = ref(false)
const source = ref('')

const open = (pdf) => {
  source.value = pdf;
  show.value = true
}
const close = () => {
  source.value = '';
  show.value = false
}

onMounted(() => {
  window.SituRecorder.startRecord({
    baseUrl: 'https://tpcxwyhs-test.tpi.cntaiping.com',
    recordPerTime: 20,
    recordCanvasToBase64: true
  });
})
</script>

<template>
  <div>
    <div>
      <button type="button" @click="open('/C00002632512021083012023.pdf')">查看条款（40页）</button>
    </div>
  </div>
  <Pdf v-if="show" :source="source" @close="close" />
</template>

<style scoped>

</style>
