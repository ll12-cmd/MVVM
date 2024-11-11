<template>
  <title>动态更新和删除列表项</title>
  <h1>动态列表管理</h1>
    <ul id="myList">
        <li v-for="(name, index) in names" :key="index">{{ name }}
            <button @click="editList(index)">编辑</button>
            <button @click="removeList(index)">删除</button>
        </li>
    </ul>
    <div class = "input-content">
        <input type="text" id="itemInput" placeholder="新项" v-model="newList">
        <button id="addItem" @click="addList()">添加项</button>
    </div>

</template>

   
<script setup>
import { ref } from 'vue'//引入ref

//两个响应式对象
const names =ref([])
const newList =ref('')

//点击事件,修改h1内容及时间

//添加操作
const addList = ()=>{
    if(newList.value.trim()===''||newList.value===null){
        alert("输入不能为空，请输入姓名！")
    }
    else {
        names.value.push(newList.value)
        //将输入值置为空，防止对后续的添加造成干扰
        newList.value=''
    }
    
}

//编辑操作(！！！使用splice可以删除原数据并添加新数据即编辑该数据！！！)
const editList = index=>{
    const newName = prompt("请输入新的姓名：", names.value[index]);
    while(newName.trim()===''||newName===null){
        alert("输入不能为空，请输入新的姓名！")
        newName = prompt("请重新输入新的姓名：", names.value[index]);
    }
    names.value.splice(index,1,newName)
}

//删除操作
const removeList = index =>{
    names.value.splice(index,1)
}

</script>


<style scoped>
    body {
        font-family: Arial, sans-serif;
        background-color: #f4f4f4;
        margin: 0;
        padding: 20px;
    }
    h1 {
        text-align: center;
        color: #333;
    }
    ul {
        list-style-type: none;
        padding: 0;
        max-width: 600px;
        margin: 20px auto;
        background: white;
        border-radius: 5px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
    li {
        padding: 15px;
        border-bottom: 1px solid #ddd;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    li:last-child {
        border-bottom: none;
    }
    button {
        background-color: #007BFF;
        color: white;
        border: none;
        border-radius: 5px;
        padding: 8px 12px;
        cursor: pointer;
        transition: background-color 0.3s;
    }
    button:hover {
        background-color: #0056b3;
    }
    input[type="text"] {
        padding: 10px;
        width: 500px;
        border: 1px solid #ccc;
        border-radius: 5px;
        margin-right: 10px;
    }
    .input-content {
        display: flex;
        justify-content: center;
        margin-top: 20px;
    }

</style>