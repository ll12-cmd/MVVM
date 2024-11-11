<template>
     <title>动态改变文档内容</title>
    <div>
        <h1>{{ title }}</h1>
        <button @click="showCurrentTimeAndChangeTitle()">改变标题</button>
        <div>{{ currentTime }}</div>
    </div>

</template>

    
<script setup>
import { ref } from 'vue'//引入ref

//两个响应式对象
const title = ref('初始标题')
const currentTime = ref() 

//点击事件,修改h1内容及时间
const showCurrentTimeAndChangeTitle = () => {
    title.value = '欢迎来到我的网站'
    currentTime.value = new Date().toLocaleString() // 更新当前时间
}

</script>


<style scoped>


</style>