<template>

  <title>表格数据排序</title>
  <table id="myTable">
    <thead>
      <tr>
        <th>姓名</th>
        <th>年龄</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(person, index) in sortPeople" :key="index">
        <td @click="updateName(index)">{{person.name}}</td>
        <td @click="updateAge(index)">{{ person.age }}</td>
        <td><button @click="removeRow(index)">删除</button></td>
      </tr>
    </tbody>
    
  </table>
  <input type="text" id="nameInput" v-model="nameInput" placeholder="姓名" />
  <input type="number" id="ageInput" v-model="ageInput" placeholder="年龄" />
  <button id="addRow"class="add-button" @click="addRow()">添加数据</button>

</template>

    
<script setup>
import { ref ,computed} from 'vue'//引入ref

//两个响应式对象
const nameInput =ref('')
const ageInput=ref(null)
const people=ref([])

//按年龄排序
const sortPeople = computed(() => {
      return [...people.value].sort((a, b) => a.age - b.age);
    });

//点击事件
//添加操作
const addRow =()=>{
  if(nameInput.value===''){
    alert("姓名不能为空，请输入姓名！")
  }
  else if(ageInput.value===null){
    alert("年龄不能为空，请输入年龄！")
  }
  else if(ageInput.value<0||ageInput.value>=120){
    alert("年龄在0-120岁之间，请重新输入年龄！")
  }
  else {
    //将值加入people（name,age）中
        people.value.push({ name: nameInput.value, age: ageInput.value });
        //加入后将姓名和年龄置为空，防止扰乱后续的添加操作
        nameInput.value = '';
        ageInput.value = null;
  }
}

//删除操作
const removeRow =index=>{
  people.value.splice(index,1);
}

//编辑修改姓名操作(！！！直接对数组进行赋值修改！！！)
const updateName = index=>{
    const newName = prompt("请输入新的姓名：", people.value[index].name);
    while(newName.trim()===''){
        alert("输入不能为空，请输入新的姓名！")
        newName = prompt("请重新输入新的姓名：",people.value[index].name);
    }
    people.value[index].name = newName
}

//编辑修改年龄操作(！！！直接对数组进行赋值修改！！！)
const updateAge= index=>{
    const newAge = prompt("请输入新的年龄：", people.value[index].age);
    if(newAge.trim()===''){
        alert("输入不能为空，请输入新的年龄！")
        newAge = prompt("请重新输入新的年龄：",people.value[index].age);
    }
    people.value[index].age = newAge
}



</script>


<style scoped>
table {
    width: 50%;
    margin-top: 20px;
    border: 1px solid #ddd;
  }

  th {
    background-color: #dfeefd;
  }

  th,
  td {
    padding: 8px;
    text-align: left;
  }

  tr:nth-child(even) {
    background-color: #f2f2f2;
  }
  
  .add-button{
    margin-top: 20px;
  }

</style>