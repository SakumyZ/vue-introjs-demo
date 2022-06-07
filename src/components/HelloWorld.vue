<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'
import introJs from 'intro.js'

defineProps<{ msg: string }>()

const guide = () => {
  introJs()
    .setOptions({
      steps: [
        {
          title: 'Welcome',
          element: document.querySelector('.step_1')!,
          intro: 'This step focuses on an image',
          position: 'right'
        },
        {
          title: 'Farewell!',
          element: document.querySelector('.step_2')!,
          intro: 'And this is our final step!',
          position: 'right'
        }
      ],
      nextLabel: '下一个', // 下一个按钮文字
      prevLabel: '上一个', // 上一个按钮文字
      skipLabel: '跳过', // 跳过按钮文字
      doneLabel: '立即体验', // 完成按钮文字
      hidePrev: true, // 在第一步中是否隐藏上一个按钮
      hideNext: true, // 在最后一步中是否隐藏下一个按钮
      exitOnOverlayClick: false, // 点击叠加层时是否退出介绍
      showStepNumbers: false, // 是否显示步骤编号
      disableInteraction: false, // 是否禁用与突出显示的框内的元素的交互，就是禁止点击
      showBullets: true // 是否显示面板指示点
    })
    .start()
}

onMounted(() => {
  nextTick(() => {
    guide()
  })
})

const count = ref(0)
</script>

<template>
  <h1 class="step_1">{{ msg }}</h1>

  <p>
    Recommended IDE setup:
    <a href="https://code.visualstudio.com/" target="_blank">VS Code</a>
    +
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
  </p>

  <p>See <code>README.md</code> for more information.</p>

  <p class="step_2">
    <a href="https://vitejs.dev/guide/features.html" target="_blank"> Vite Docs </a>
    |
    <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Docs</a>
  </p>

  <button type="button" @click="count++">count is: {{ count }}</button>
  <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p>
</template>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
