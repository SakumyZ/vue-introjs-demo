<script setup lang="ts">
import { defineProps, defineEmits, ref, nextTick } from 'vue'

// 定义 prop
defineProps({
  title: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['update:title'])

// 标题
const cardTitleInputRef = ref<HTMLInputElement | null>(null)
const isShowTitleInput = ref<Boolean>(false)

// 点击修改标题
const handleEditTitle = () => {
  isShowTitleInput.value = true

  nextTick(() => {
    cardTitleInputRef.value?.focus()
  })
}
// 标题 input 框 focusout 处理
const handleTitleFoucusout = () => {
  isShowTitleInput.value = false
}
// 标题部分数据变更，更新双向绑定
const handleChangeTitle = (e: Event) => {
  // 在 双向绑定的 prop 被修改时派发 update 事件
  emit('update:title', (e.target as HTMLInputElement).value)
}
</script>

<template>
  <div class="card">
    <div class="card_header">
      <input
        v-if="isShowTitleInput"
        ref="cardTitleInputRef"
        type="text"
        :value="title"
        @focusout="handleTitleFoucusout"
        @change="handleChangeTitle"
      />
      <span v-else>{{ title }}</span>
      <span @click="handleEditTitle">点击修改</span>
    </div>
    <div class="card_body"></div>
  </div>
</template>

<style scoped>
.card {
  width: 300px;
  height: 200px;
  border: 1px solid #000;
}

.card_header {
  border-bottom: 1px solid #000;
  height: 40px;
}
</style>
