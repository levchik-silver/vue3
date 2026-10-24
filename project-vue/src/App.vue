<template>
  <div>
    <h1>Сотрудники</h1>

    <h2>Добавить сотрудника</h2>
    <div>
      <input v-model="formName" placeholder="Имя" />
      <input v-model.number="formAge" type="number" placeholder="Возраст" />

      <select v-model="formDepartment">
        <option value="">-- отдел --</option>
        <option v-for="dep in departments" :key="dep" :value="dep">{{ dep }}</option>
      </select>

      <input v-model.number="formSalary" type="number" placeholder="Зарплата" />

      <label>
        <input v-model="formActive" type="checkbox" /> Работает
      </label>

      <span>Навыки:</span>
      <label v-for="skill in allSkills" :key="skill">
        <input v-model="formSkills" type="checkbox" :value="skill" /> {{ skill }}
      </label>

      <button :disabled="!isFormValid" @click="addEmployee">Добавить</button>
    </div>

    <h2>Поиск и фильтры</h2>
    <div>
      <input v-model="searchName" placeholder="Поиск по имени" />

      <select v-model="filterDepartment">
        <option value="">Все отделы</option>
        <option v-for="dep in departments" :key="dep" :value="dep">{{ dep }}</option>
      </select>

      <select v-model="filterStatus">
        <option value="all">Все сотрудники</option>
        <option value="active">Только работающие</option>
        <option value="fired">Только уволенные</option>
      </select>
    </div>

    <table border="1">
      <thead>
        <tr>
          <th>ID</th><th>Имя</th><th>Возраст</th><th>Отдел</th>
          <th>Зарплата</th><th>Статус</th><th>Навыки</th><th>Действия</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="emp in filteredEmployees" :key="emp.id">
          <template v-if="editingId === emp.id">
            <td>{{ emp.id }}</td>
            <td><input v-model="editForm.name" /></td>
            <td><input v-model.number="editForm.age" type="number" /></td>
            <td>
              <select v-model="editForm.department">
                <option v-for="dep in departments" :key="dep" :value="dep">{{ dep }}</option>
              </select>
            </td>
            <td><input v-model.number="editForm.salary" type="number" /></td>
            <td>
              <span v-if="emp.active">Работает</span>
              <span v-else>Уволен</span>
            </td>
            <td>{{ emp.skills.join(', ') }}</td>
            <td>
              <button @click="saveEdit(emp.id)">Сохранить</button>
              <button @click="editingId = null">Отмена</button>
            </td>
          </template>

          <template v-else>
            <td>{{ emp.id }}</td>
            <td>{{ emp.name }}</td>
            <td>{{ emp.age }}</td>
            <td>{{ emp.department }}</td>
            <td>{{ emp.salary }}</td>
            <td>
              <span v-if="emp.active">Работает</span>
              <span v-else>Уволен</span>
            </td>
            <td>{{ emp.skills.join(', ') }}</td>
            <td>
              <button @click="startEdit(emp)">Редактировать</button>
              <button v-if="emp.active" @click="toggleStatus(emp.id)">Уволить</button>
              <button v-else @click="toggleStatus(emp.id)">Восстановить</button>
              <button @click="removeEmployee(emp.id)">Удалить</button>
            </td>
          </template>
        </tr>
        <tr v-if="filteredEmployees.length === 0">
          <td colspan="8">Сотрудники не найдены</td>
        </tr>
      </tbody>
    </table>

    <h2>Статистика</h2>
    <p>Всего: {{ totalCount }}</p>
    <p>Работают: {{ activeCount }}</p>
    <p>Уволены: {{ firedCount }}</p>
    <p>Сумма зарплат: {{ totalSalary }}</p>
    <p>Средняя зарплата: {{ averageSalary }}</p>
  </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

const departments = ['IT', 'Дизайн', 'Покупки', 'Финансы']
const allSkills = ['JavaScript', 'Vue', 'Python', 'Блендер']

const employees = ref([
  { id: 1, name: 'Иван', age: 28, department: 'IT', salary: 80000, active: true, skills: ['JavaScript', 'Vue'] },
  { id: 2, name: 'Мария', age: 34, department: 'Покупки', salary: 60000, active: true, skills: ['яПОКУПИКМ'] },
  { id: 3, name: 'Сергей', age: 45, department: 'ФИнаны', salary: 70000, active: false, skills: ['Python'] },
])

const formName = ref('')
const formAge = ref(null)
const formDepartment = ref('')
const formSalary = ref(null)
const formActive = ref(true)
const formSkills = ref([])

const isFormValid = computed(() => {
  if (formName.value.trim() === '') return false
  if (formAge.value === null || formAge.value < 18) return false
  if (formDepartment.value === '') return false
  if (formSalary.value === null || formSalary.value <= 0) return false
  return true
})

let nextId = 4

function addEmployee() {
  if (!isFormValid.value) return

  const newEmployee = {
    id: nextId,
    name: formName.value,
    age: formAge.value,
    department: formDepartment.value,
    salary: formSalary.value,
    active: formActive.value,
    skills: [...formSkills.value],
  }

  employees.value.push(newEmployee)
  nextId = nextId + 1

  formName.value = ''
  formAge.value = null
  formDepartment.value = ''
  formSalary.value = null
  formActive.value = true
  formSkills.value = []
}

function removeEmployee(id) {
  employees.value = employees.value.filter(e => e.id !== id)
}

function toggleStatus(id) {
  const emp = employees.value.find(e => e.id === id)
  emp.active = !emp.active
}

const editingId = ref(null)
const editForm = reactive({ name: '', age: null, department: '', salary: null })

function startEdit(emp) {
  editingId.value = emp.id
  editForm.name = emp.name
  editForm.age = emp.age
  editForm.department = emp.department
  editForm.salary = emp.salary
}

function saveEdit(id) {
  const emp = employees.value.find(e => e.id === id)
  emp.name = editForm.name
  emp.age = editForm.age
  emp.department = editForm.department
  emp.salary = editForm.salary
  editingId.value = null
}

const searchName = ref('')
const filterDepartment = ref('')
const filterStatus = ref('all')

const filteredEmployees = computed(() => {
  const result = []

  for (const emp of employees.value) {
    if (!emp.name.toLowerCase().includes(searchName.value.toLowerCase())) continue
    if (filterDepartment.value !== '' && emp.department !== filterDepartment.value) continue
    if (filterStatus.value === 'active' && !emp.active) continue
    if (filterStatus.value === 'fired' && emp.active) continue

    result.push(emp)
  }

  return result
})

const totalCount = computed(() => employees.value.length)
const activeCount = computed(() => employees.value.filter(e => e.active).length)
const firedCount = computed(() => employees.value.filter(e => !e.active).length)
const totalSalary = computed(() => employees.value.reduce((s, e) => s + e.salary, 0))
const averageSalary = computed(() =>
  employees.value.length ? Math.round(totalSalary.value / employees.value.length) : 0
)
</script>
