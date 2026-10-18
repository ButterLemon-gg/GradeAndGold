<template>
  <div class="container">
    <h1>แบบฝึกหัดที่ 16 Vue.js</h1>
    
    <!-- ปุ่มสลับหน้าเว็บ -->
    <div class="nav-menu">
      <button 
        @click="currentTab = 'grade'" 
        :class="{ active: currentTab === 'grade' }" class="btn">
        1. ตัดเกรด
      </button>
      <button 
        @click="currentTab = 'gold'" 
        :class="{ active: currentTab === 'gold' }" class="btn">
        2. ดึงราคาทอง
      </button>
    </div>

    <!-- แสดง Component ตามปุ่มที่เลือก -->
    <component :is="currentTab === 'grade' ? GradeComponent : GoldComponent" />
  </div>
</template>

<script>
import GradeComponent from './components/Grade.vue'
import GoldComponent from './components/Gold.vue'

export default {
  name: 'App',
  data() {
    return {
      currentTab: 'grade',
      GradeComponent,
      GoldComponent
    }
  }
}
</script>

<style>
body {
    font-family: sans-serif;
    padding: 20px;
    background-color: #f5f5f5;
}
.container {
    max-width: 500px;
    margin: auto;
}
.btn {
    padding: 8px 12px;
    margin-right: 5px;
    border-radius: 4px;
    background: #ddd;
    color: black;
    border: none;
    cursor: pointer;
    font-weight: bold;
}
.btn.active {
    background: #007bff;
    color: white;
}
.nav-menu {
    margin-bottom: 20px;
}
</style>