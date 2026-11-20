<script setup>
import EmployeeList from './components/EmployeeList.vue'
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light border-bottom">
    <div class="container">
      <a class="navbar-brand fw-semibold" href="#">ระบบข้อมูลพนักงาน</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <a class="nav-link" href="#">หน้าหลัก</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active fw-semibold" aria-current="page" href="#">ข้อมูลพนักงาน</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <EmployeeList />
</template>

<style>
body {
  font-family: 'Leelawadee UI', Tahoma, sans-serif;
  background-color: #ffffff;
}
</style>
