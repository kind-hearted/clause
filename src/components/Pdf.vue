<script setup>
import { defineProps, defineEmits, ref, onMounted, onUnmounted } from 'vue'
import VuePdfEmbed from 'vue-pdf-embed'

const { source } = defineProps(['source'])

const emit = defineEmits(['close'])

const countdown = ref(10)

onMounted(() => {
  const timer = setInterval(() => {
    if (countdown.value === 0) {
      clearInterval(timer)
      return
    }
    countdown.value = countdown.value - 1
  }, 1000);
})

</script>

<template>
  <div class="dialog">
    <div class="title"><button type="button" class="back" @click="$emit('close')">返回</button>保险条款</div>
    <div class="pdf">
      <vue-pdf-embed :disable-text-layer="true" :source="source" />
    </div>
    <div class="button"><button type="button" @click="$emit('close')">我已阅读并同意（{{countdown}}秒）</button></div>
  </div>
  <div class="mask"></div>
</template>

<style scoped>
.dialog {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 501px;
  z-index: 2002;
  border-top: 1px solid red;
  background: #fff;
}
.title {
  position: relative;
  height: 30px;
  line-height: 30px;
  border-bottom: 1px solid red;
  text-align: center;
}
.back {
  position: absolute;
  top: 0;
  left: 0;
  text-align: center;
}
.pdf {
  height: 435px;
  overflow-y: auto;
  overflow-x: hidden;
}
.button {
  text-align: center;
  height: 30px;
  color: #fff;
  background: #81C0FF;
  border: 0.01333rem solid #81C0FF;
}
.mask {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: black;
  opacity: 0.3;
  z-index: 2000;   
}
</style>
