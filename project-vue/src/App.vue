<template>
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
const techs = ['Vue', 'JS', 'css']

const name = ref('')
const age = ref(null)
const city = ref('')
const dir = ref('')
const tech = ref([])
const about = ref('')
const ok = ref(false)
const show = ref(false)
</script>
