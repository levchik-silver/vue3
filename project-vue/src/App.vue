<!-- <template>
  <div class="student-card">
    <h1>Страница студентов</h1>
    <ul>
      <li><strong>Имя:</strong> {{ name }}</li>
      <li><strong>Город:</strong> {{ city }}</li>
       <li><strong>Возраст:</strong> {{ age }}</li>
      <li><strong>Направление обучения:</strong> {{ direction }}</li>
    </ul>
    <br>
    <ul>
      <li><strong>Имя:</strong> {{ name1 }}</li>
      <li><strong>Возраст:</strong> {{ age1 }}</li>
      <li><strong>Город:</strong> {{ city1 }}</li>
      <li><strong>Направление обучения:</strong> {{ direction1 }}</li>
    </ul>
      <br>
    <ul>
      <li><strong>Имя:</strong> {{ name2 }}</li>
      <li><strong>Возраст:</strong> {{ age2 }}</li>
      <li><strong>Город:</strong> {{ city2 }}</li>
      <li><strong>Направление обучения:</strong> {{ direction2 }}</li>
    </ul>
    <br>
    <ul>
      <li><strong>Имя:</strong> {{ name3 }}</li>
      <li><strong>Возраст:</strong> {{ age3 }}</li>
      <li><strong>Город:</strong> {{ city3 }}</li>
      <li><strong>Направление обучения:</strong> {{ direction3 }}</li>
    </ul>
    <br>
    <ul>
      <li><strong>Имя:</strong> {{ name4 }}</li>
      <li><strong>Возраст:</strong> {{ age4 }}</li>
      <li><strong>Город:</strong> {{ city4 }}</li>
      <li><strong>Направление обучения:</strong> {{ direction4 }}</li>
    </ul>
    <br>
    <ul>
      <li><strong>Имя:</strong> {{ name5 }}</li>
      <li><strong>Возраст:</strong> {{ age5 }}</li>
      <li><strong>Город:</strong> {{ city5 }}</li>
      <li><strong>Направление обучения:</strong> {{ direction5 }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const name = ref('Антон Мухов')
const age = ref(21)
const city = ref('Краснодар')
const direction = ref('Прогромирования')

const name1 = ref('А G H')
const age1 = ref(21)
const city1 = ref('Краснодар')
const direction1 = ref('Прогромирования')

const name2 = ref('R SDG EW')
const age2 = ref(21)
const city2 = ref('Краснодар')
const direction2 = ref('Прогромирования')
</script>

<style scoped>
.student-card {
  max-width: 400px;
  margin: 40px auto;
  padding: 24px;
  border: 1px solid #fafafa;
  border-radius: 12px;
  font-family: sans-serif;
  background: #000000;
}
.student-card h1 {
  font-size: 1.4rem;
  margin-bottom: 16px;
}
.student-card ul {
  list-style: none;
  padding: 0;
}
.student-card li {
  padding: 8px 0;
  border-bottom: 1px solid #ffffff;
}
.student-card strong {
  display: inline-block;
  width: 200px;
}
</style> -->

<!-- <script setup>
 import {ref, reactive} from 'vue'
 const items = ref ([1,2,3,4,5])
</script>
<template>
  <ul>
    <li v-for="(item,index) in items" :key="item.id">
      {{ index }}:{{ item }}
    </li>
  </ul>
</template> -->

<!-- <script setup>
 import {ref, reactive} from 'vue'
 const task = ref ([
  {id:1,text:"fff",done:false},
  {id:2,text:"ggg",done:true},
  {id:3,text:"ddd",done:false},
  ])
</script>
<template>
  <h1>мои дела</h1>
  <ul>
    <li v-for="task in task" :key="task.id">
      {{task.done?"Ok":"No"}} {{ task.text }}
    </li>
  </ul>
</template> -->


<!-- 
<script setup>

import{ref} from 'vue'
const tasks=ref([])
const newTask=ref('')
const filter = ref('')
const visibleTasks = computed(()=>{
  if(filter.value==='active')return tasks.value.filter(t=>!t.done)
  if(filter.value==='done')return tasks.value.filter(t=>t.done)
})
const stats = computed(()=>({
  total:tasks.value.length,
  done:tasks.value.filter(t=>t.done).length
}))
function addTask(){
    if(newTask.value.trim()==='')return
    tasks.value.push({
        id:Date.now(),
        text:newTask.value,
        done:false,
    })
    newTask.value=''
}
function removeTask(id){
    tasks.value=tasks.value.filter(t=>t.id!==id)
}
</script>

<template>
    <h1>мои дела</h1>
    <input v-model="newTask" placeholder="новое задание" @keyup.enter="addTask"/>
    <button @click="addTask">добавить</button>
    <button @click="filter='all'">все</button>
    <button @click="filter='active'">активные</button>
    <button @click="filter='done'">выполненые</button>
    <p>Выполнено: {{ stats.done }} из {{ stats.total }}</p>
    <ul>
        <li v-for="task in visibleTasks" :key="task.id">
          <input type="checkbox" v-model="task.done">
            {{ task.text }} <button @click="removeTask(task.id)">Удалить</button>
        </li>
    </ul>

</template>
<style scoped>
h1{
    color: blueviolet;
}
</style> -->


<!-- <script setup>
import { ref, computed } from 'vue'

const games = ref([
  { title: 'Minecraft',     easy: true,  done: true,  rating: 9.0 },
  { title: 'Stalker', easy: true,  done: true,  rating: 9.5 },
  { title: 'Portal 2',       easy: true,  done: false, rating: 9.7 },
  { title: 'Rust',  easy: false, done: false, rating: 9.8 },
  { title: 'Standoff2',     easy: false, done: false, rating: 9.6 }
])

const onlyEasy = ref(false)

const list = computed(() =>
  games.value
    .filter(g => !onlyEasy.value || g.easy)
    .sort((a, b) => b.rating - a.rating)
)

const percent = computed(() => {
  const done = games.value.filter(g => g.done).length
  return Math.round(done / games.value.length * 100)
})
</script>

<template>
  <h1>Мои игры</h1>

  <p>Пройдено: {{ percent }}%</p>
  <progress :value="percent" max="100"></progress>

  <p>
    <label>
      <input type="checkbox" v-model="onlyEasy" />
      Только для новичков
    </label>
  </p>

  <ul>
    <li v-for="(g, i) in list" :key="g.title">
      {{ i + 1 }}. {{ g.title }} — ⭐ {{ g.rating }}
      <button @click="g.done = !g.done">
        {{ g.done ? 'да' : 'нет' }}
      </button>
    </li>
  </ul>
</template>

<style>
body { font-family: sans-serif; max-width: 500px; margin: 30px auto; }
li { margin: 6px 0; }
progress { width: 100%; height: 14px; }
</style> -->
<!-- <script setup>
 import{ref,computed} from 'vue'
 const isVisible=ref(true)
 function hide(){
  isVisible.value=!isVisible.value
 }
</script>
<template>
  <p v-if="isVisible">
   ff
  </p>
 <button @click="hide">

 </button>
</template> -->
<!-- <script setup>
 import{ref,computed} from 'vue'
const temp = ref(25)
</script>
<template>
  <h2 v-if="temp<=15">
    🥶
  </h2>
  <h2 v-else-if="temp>35 || temp<25">
    тепло
  </h2>
  <h2 v-else>
    жарко
  </h2>
</template> -->


<!-- <script setup>
import{ref,computed} from 'vue'
const fruits=["яблоко","банан","апельсин"]
</script>
<template>
    <h2>
        Фрукты
    </h2>
    <h4 v-for="(fruit,index) in fruits">
        {{ index +1 }}-{{ fruit }}
    </h4>
</template>
<style scoped>
h1{
    color: blueviolet;
}
</style> -->

<!-- <script setup>
import{ref,computed} from 'vue'
const students=[
  {
    id:1,
    name:'Cheese',
    price:58
  },
  {
    id:2,
    name:'Bread',
    price:79
  },
  {
    id:3,
    name:'Lemon',
    price:12
  }
]
</script>
<template>
 <div class="card" v-for="student in students":key="student.id">
  
  <h2 >
    {{ student.name }}
  </h2>
  
  <p class="e">
 Price:{{ student.price }}
  </p>
 </div>
</template>
<style scoped>
h1{
    color: blueviolet;
}
.card{
  display: flex;
  justify-content: space-between;
  border: 1px solid black ;
  width: 100px;
  height: 123px;
}
.e{
 display: flex;
 justify-content: space-between;
}

</style> -->
<!-- <script setup>
import{ref,computed} from 'vue'
const students=[
  {
    id:1,
    name:'Aboba',
    pos:true
  },
  {
    id:2,
    age:'Aboba2',
     pos:false
  }
]
function addStudent(){
  students.value.push({
    id:3,
    name:"Aboba3"
  })
}
function deleteStudent(id){
  students.value=students.value.filter(student=>student.id!==id)
}
</script>
<template>
 <div v-for="student in students":key="student.id">
  <span v-if="student.pos">{{ student.name }}</span>
  <button @click="deleteStudent(student.id)">delete</button>
  <p v-for="(value,key) in student">
  {{ key }}:{{ value }}
  </p>
 </div>
 <button @click="addStudent">add</button>
</template>
<style scoped>
h1{
    color: blueviolet;
}


</style> -->

<!-- <script setup>
import{ref,computed} from 'vue'
const name = ref ('')
function showName(){
  alert(name.value)
}
</script>

<template>
  <input v-model="name" type="text" placeholder="inputname">
  <button @click="showName">Show</button>
</template> -->

<!-- <script setup>
import{ref,computed} from 'vue'
const age = ref (0)
const text = ref ('')
function showName(){
  alert(age.value+1)
}
function showText(){
  alert(text.value)
}
</script>

<template>
  <input v-model="age" type="number" placeholder="input age">
  <button @click="showName">Show</button>
  <textarea v-model="text"></textarea>
  <p>{{ text }}</p>
  <button @click="showText">Show</button>
</template> -->
<!-- <script setup>
import{ref,computed} from 'vue'
const age=ref(0)
const text=ref('')
const agree=ref('')
function showName(){
    alert(age.value+1)
}
function showText(){
    alert(text.value)
}
</script>
<template>
<label>
    <input v-model="agree" type="radio" value="aboba">
    я согласен
</label>
<p>{{ agree }}</p>
</template>
<style scoped>
h1{
    color: blueviolet;
}
</style> -->

<!-- <template>
  <div>
    <p>Имя: <input v-model="name" /></p>

    <p>Возраст: <input v-model.number="age" type="number" /></p>

    <p>
      Город:
      <select v-model="city">
        <option v-for="c in cities" :key="c">{{ c }}</option>
      </select>
    </p>

    <p>
      Направление:
      <label v-for="d in dirs" :key="d">
        <input v-model="dir" type="radio" :value="d" /> {{ d }}
      </label>
    </p>

    <p>
      Технологии:
      <label v-for="t in techs" :key="t">
        <input v-model="tech" type="checkbox" :value="t" /> {{ t }}
      </label>
    </p>

    <p>О себе: <textarea v-model="about"></textarea></p>

    <p>
      <label>
        <input v-model="ok" type="checkbox" /> Согласен с правилами
      </label>
    </p>

    <button :disabled="!ok" @click="show = true">Зарегистрироваться</button>

    <pre v-if="show">{{ { name, age, city, dir, tech, about } }}</pre>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const cities = ['Москва', 'Казань', 'Сочи']
const dirs = ['Вперед', 'назад']
const techs = ['Vue', 'JS', 'сss']

const name = ref('')
const age = ref(null)
const city = ref('')
const dir = ref('')
const tech = ref([])
const about = ref('')
const ok = ref(false)
const show = ref(false)
</script> -->

<!-- <script setup>
import{ref, computed} from 'vue'
const name = ref('')
const number = ref()
</script>
<template>
  <label>
    Имя
  <input type="text" v-model="name">
  <br>
  </label>
<label>
  Возвраст
  <input type="number" v-model="number">
</label>
<button :disabled="!name || !number" >reply</button>
</template> -->
 <!-- <script setup>
import{ref, computed} from 'vue'
const isDisable= ref(false)
function dispinput(){
  isDisable.value=!isDisable.value
}
</script>
<template>
  <label>
    Имя
  <input type="text" :disabled="isDisable">
  <br>
  </label>
<input @click="dispinput" type="checkbox" >{{ isDisable?'unblock' : 'block' }}</input>
</template>  -->


<!-- <script setup>
import{ref,computed} from 'vue'
const items=ref(["Aboba","bOb"])
const text=ref('')
function addItems(){
    items.value.push(text.value)
}
function deleteItems(id){
  items.value=items.value.filter(i=>item.id!==id)
}
</script>
<template>
    <ul>
        <li v-for="(item,index) in items":key="index">
            {{ item }}
        </li>
    </ul>
    <label>
        <input type="text" v-model="text">
        имя
    </label>

<button @click="addItems">
    добавить
</button>

</template>
<style scoped>
h1{
    color: blueviolet;
}
</style> -->

<!-- 
<script setup>
import { ref, computed } from 'vue'

const items = ref(["Aboba", "bOb"])
const text = ref('')


const users = ref([
  { id: 1, name: 'name1', salary: 100, age: 30 },
  { id: 2, name: 'name2', salary: 200, age: 40 }, 
  { id: 3, name: 'name3', salary: 300, age: 50 },
])


const addItems = () => {
  if (text.value.trim()) {
    items.value.push(text.value)
    text.value = ''
  }
}


const removeUser = (id) => {
  users.value = users.value.filter(user => user.id !== id)
}
</script>

<template>

  <ul>
    <li v-for="(item, index) in items" :key="index" @click="items.splice(index, 1)">
      {{ item }}
    </li>
  </ul>

  <label>
    <input type="text" v-model="text">
    имя
  </label>
  

  <button @click="addItems">добавить</button>

  <hr>


  <h3>Список работников</h3>
  <table border = "1">
    <thead>
      <tr>
        <th>ID</th>
        <th>Имя</th>
        <th>Зарплата</th>
        <th>Возраст</th>
        <th>Действие</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="user in users" :key="user.id">
        <td>{{ user.id }}</td>
        <td>{{ user.name }}</td>
        <td>{{ user.salary }}</td>
        <td>{{ user.age }}</td>
        <td>
          <button @click="removeUser(user.id)">Удалить</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
  h1 {
    color: blueviolet;
  }
  table {
    width: 100%;
    border-collapse: collapse;
  }
  th, td {
    padding: 8px;
    text-align: left;
    border: 1px solid #ccc;
  }
  th {
    background-color: #f5f5f5;
  }
</style> -->

<!-- <script setup>
import{ref,computed} from 'vue'
const active = ref(true)
</script>
<template>
  <div :class="{active}">
     user
  </div>
  <button @click="active=!active">
    change style
  </button>
</template>
<style scoped>
div{
  width:200px;
  padding: 20px;
  background: gray;
}
.active{
  background: greenyellow;
  color: aliceblue;
  font-weight: bold;
}
</style> -->

<!-- <script setup>
import{ref,computed} from 'vue'
const isActive = ref(true)
const hasError = ref(false)
</script>
<template>
  <p :class="isActive?'success':'error'">
  gg
  </p>


</template>
<style scoped>
.success{
  background: rgb(174, 255, 0);
}
.error{
  color: brown;
}
</style> -->

<!-- <script setup>
import{ref,computed} from 'vue';
const wokup = ref(true)
const disable = ref(false)
const employees=ref([
  {
    id:1,
    name:"aboba",
    active:true
  },
  {
    id:2,
    name:"aboba2",
    active:false
  }
])
</script>
<template>
  <div v-for="employye in employees":key="employye.id" class="employee" :class="{working:employye.active,nerab:!employye.active}">
    {{ employye.name }}
    <span v-if="employye.active">workig</span>
    <span v-else>leave</span>
     <button @click="employye.active=!employye.active">удалить:работать</button>
  </div>

  

</template>
<style scoped>
.employee{
  width: 200px;
  padding: 15px;
  margin: 10px;
  border: 1px border black;
  
}
.working{
  background-color: brown;
  color: black;
}
.nerab{
  background-color: aqua;
  color:aliceblue
}
</style> -->
<!-- <script setup>
import {ref,computed} from 'vue'
const name=ref('')
const age= ref (0)
function Send (){
  console.log(name.value)
  console.log(age.value)
}
</script>
<template>
  <form @submit.prevent="Send">
   <input
   v-model="name"
   type="text"
   placeholder="Enter name"
   >
    <input
   v-model="age"
   type="number"
   placeholder="Enter age"
   >
   <input type="checkbox" v-model="agree">
   <button type="submit">Press</button>
  </form>
</template> -->


<!-- <script setup>
import { ref, computed } from 'vue'
const num=ref('')
const result=ref(0)
function calc(){
  result.value=num.value*num.value
}
</script>
<template>
  <input type="number"
  v-model.number="num"
  placeholder="введите число">
      <button @click="calc">
        Вычислить квадрат
      </button>
      <p>
         результат: {{ result }}
      </p>
  </template>
<style scoped>

</style> -->


<!-- <script setup>
import { ref, computed } from 'vue'
const city=ref('')
</script>
<template>
 <select v-model="city">
  <option value="">choose your city</option>
  <option value="Krasnodar">Krasnodar</option>
  <option value="Moscow">Moscow</option>
  <option value="Sochy">Sochy</option>
 </select>
 <p>
  you're choose:{{ city }}
 </p>
  </template>
<style scoped>

</style> -->

<script setup>
import { ref, computed } from 'vue'
const cities=[
  "Krasnodar",
  "sochi",
  "Moscow",
  "peter"
]
const month=[
  'Январь',
  'Февраль',
  'Март',
  ''
]
const city=ref('')
</script>
<template>
  <select v-model="city">
    <option value="">choose your city</option>
    <option v-for="item in cities":key='item':value="item">{{ item }}</option>
  </select>
   <p>
    you're choose: {{city}} 
  </p>
  </template>
 
<style scoped>

</style>

