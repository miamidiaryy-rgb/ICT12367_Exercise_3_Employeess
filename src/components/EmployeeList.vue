<script setup>
import { ref, computed } from 'vue'

const searchText = ref('')
const selectedDept = ref('')

const employees = ref([
  {
    id: 'EMP001',
    name: 'สมชาย ใจดี',
    position: 'โปรแกรมเมอร์',
    department: 'ไอที',
    email: 'somchai.j@company.co.th',
    phone: '081-234-5678',
    salary: 35000,
  },
  {
    id: 'EMP002',
    name: 'สุภาพร รักเรียน',
    position: 'นักวิเคราะห์ระบบ',
    department: 'ไอที',
    email: 'supaporn.r@company.co.th',
    phone: '082-345-6789',
    salary: 42000,
  },
  {
    id: 'EMP003',
    name: 'กิตติพงษ์ มั่นคง',
    position: 'เจ้าหน้าที่บุคคล',
    department: 'ทรัพยากรบุคคล',
    email: 'kittipong.m@company.co.th',
    phone: '083-456-7890',
    salary: 28000,
  },
  {
    id: 'EMP004',
    name: 'นภาพร แสงทอง',
    position: 'พนักงานบัญชี',
    department: 'บัญชีและการเงิน',
    email: 'napaporn.s@company.co.th',
    phone: '084-567-8901',
    salary: 30000,
  },
  {
    id: 'EMP005',
    name: 'ธนากร ศรีสุข',
    position: 'ผู้จัดการฝ่ายขาย',
    department: 'การขาย',
    email: 'thanakorn.s@company.co.th',
    phone: '085-678-9012',
    salary: 48000,
  },
  {
    id: 'EMP006',
    name: 'ปิยะนุช วงศ์สวัสดิ์',
    position: 'เจ้าหน้าที่การตลาด',
    department: 'การตลาด',
    email: 'piyanuch.w@company.co.th',
    phone: '086-789-0123',
    salary: 29500,
  },
  {
    id: 'EMP007',
    name: 'วรพล ชัยวัฒน์',
    position: 'ผู้ดูแลระบบเครือข่าย',
    department: 'ไอที',
    email: 'worapol.c@company.co.th',
    phone: '087-890-1234',
    salary: 38000,
  },
  {
    id: 'EMP008',
    name: 'ชุติมา พงษ์ไพศาล',
    position: 'เจ้าหน้าที่ธุรการ',
    department: 'ทรัพยากรบุคคล',
    email: 'chutima.p@company.co.th',
    phone: '089-012-3456',
    salary: 24000,
  },
])

const departments = computed(() => {
  return [...new Set(employees.value.map((emp) => emp.department))]
})

const filteredEmployees = computed(() => {
  const keyword = searchText.value.trim().toLowerCase()
  return employees.value.filter((emp) => {
    const matchDept = !selectedDept.value || emp.department === selectedDept.value
    const matchText =
      !keyword ||
      emp.id.toLowerCase().includes(keyword) ||
      emp.name.toLowerCase().includes(keyword) ||
      emp.position.toLowerCase().includes(keyword) ||
      emp.department.toLowerCase().includes(keyword)
    return matchDept && matchText
  })
})
</script>

<template>
  <div class="container mt-4 mb-5">
    <div class="d-flex flex-wrap justify-content-between align-items-center mb-3 gap-2">
      <h4 class="mb-0">ข้อมูลพนักงาน</h4>

      <div class="d-flex gap-2">
        <select v-model="selectedDept" class="form-select form-select-sm" style="width: 170px">
          <option value="">ทุกแผนก</option>
          <option v-for="dept in departments" :key="dept" :value="dept">
            {{ dept }}
          </option>
        </select>

        <input
          v-model="searchText"
          type="text"
          class="form-control form-control-sm"
          placeholder="ค้นหารหัส ชื่อ หรือตำแหน่ง..."
          style="width: 230px"
        />
      </div>
    </div>

    <div class="table-responsive">
      <table class="table table-bordered table-striped table-hover align-middle">
        <thead class="table-dark">
          <tr>
            <th scope="col" class="text-center" style="width: 60px">#</th>
            <th scope="col">รหัสพนักงาน</th>
            <th scope="col">ชื่อ-นามสกุล</th>
            <th scope="col">ตำแหน่ง</th>
            <th scope="col">แผนก</th>
            <th scope="col">อีเมล</th>
            <th scope="col">เบอร์โทรศัพท์</th>
            <th scope="col" class="text-end">เงินเดือน (บาท)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(emp, index) in filteredEmployees" :key="emp.id">
            <td class="text-center">{{ index + 1 }}</td>
            <td>{{ emp.id }}</td>
            <td>{{ emp.name }}</td>
            <td>{{ emp.position }}</td>
            <td>{{ emp.department }}</td>
            <td>{{ emp.email }}</td>
            <td>{{ emp.phone }}</td>
            <td class="text-end">{{ emp.salary.toLocaleString() }}</td>
          </tr>
          <tr v-if="filteredEmployees.length === 0">
            <td colspan="8" class="text-center text-muted py-3">ไม่พบข้อมูลพนักงาน</td>
          </tr>
        </tbody>
      </table>
    </div>

    <p class="text-muted small mb-0">
      แสดงข้อมูลทั้งหมด {{ filteredEmployees.length }} รายการ (จากพนักงานทั้งหมด {{ employees.length }} คน)
    </p>
  </div>
</template>
