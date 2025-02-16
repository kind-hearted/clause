<script setup>
import { onMounted, ref } from 'vue'
import Pdf from '@/components/Pdf.vue'

const show1 = ref(false)
const show2 = ref(false)
const source1 = ref('')
const source2 = ref(null)

const open1 = (pdf) => {
  source1.value = pdf;
  show1.value = true
}
const close1 = () => {
  source1.value = '';
  show1.value = false
}

const open2 = (pdf) => {
  source2.value = {
    // cMapUrl: 'https://unpkg.com/browse/pdfjs-dist@4.10.38/cmaps/',
    cMapUrl: '/cmaps/',
    url: pdf,
  }
  show2.value = true
}
const close2 = () => {
  source2.value = null;
  show2.value = false
}

</script>

<template>
  <div>未定义cMap</div>
  <div>
    <div>
      <button type="button" @click="open1('/C00002632512021083012023.pdf')">查看条款（40页）</button>
    </div>
  </div>
  <Pdf v-if="show1" :source="source1" @close="close1" />
  <br/>
  <div>定义cMap</div>
  <div>
    <div>
      <button type="button" @click="open2('/C00002632512021083012023.pdf')">查看条款（40页）</button>
    </div>
  </div>
  <Pdf v-if="show2" :source="source2" @close="close2" />
</template>

<style scoped>

</style>
