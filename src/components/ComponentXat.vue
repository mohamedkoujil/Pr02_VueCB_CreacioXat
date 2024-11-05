<script setup>
import ComponentMissatge from './ComponentMissatge.vue'
import { ref } from 'vue'

let missatges = ref([
  {
    idMissatge: Date.now(),
    missatge: 'Missatge prova 1',
    usuari: 'Pere'
  },
  {
    idMissatge: Date.now() + 1,
    missatge: 'Missatge prova 2',
    usuari: 'Joan'
  }
])

const autor = ref('Pere')

const onNouMissatge = (missatge) => {
  missatge.idMissatge = Date.now()
  //console.log(missatge.idMissatge)
  missatges.value.push(missatge)
}
const formatMinuts = (minuts) => {
  if (minuts < 10) {
    return 0
  }
}
</script>

<template>
  <div class="container">
    <!-- escollir un usuari -->
    <select v-model="autor" v-on:change="console.log(autor)">
      <option value="Pere">Pere</option>
      <option value="Joan">Joan</option>
    </select>

    <div class="missatgeContenedor">
      <div
        class="missatge"
        v-for="missatge in missatges"
        :key="missatge.idMissatge"
        :id="missatge.idMissatge"
      >
        <strong>{{ missatge.usuari }}:</strong> {{ missatge.missatge }}
        <div class="horaMissatge">
          <small>
            {{ new Date(missatge.idMissatge).getHours() }}:
            {{ formatMinuts(new Date(missatge.idMissatge).getMinutes()) }}
            {{ new Date(missatge.idMissatge).getMinutes() }}
          </small>
        </div>
      </div>
    </div>
    <ComponentMissatge :autor="autor" @onNouMissatge="onNouMissatge" />
  </div>
</template>

<style scoped>
.container {
  font-family: Arial, sans-serif;
  display: flex;
  flex-direction: column;
  width: 300px;
  margin: 0 auto;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

/* scroll al contenidor de missatges i scrollea automàticament */
.missatgeContenedor {
  overflow-y: auto;
  height: 200px;
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.missatgeContenedor small {
  color: #777;
}

.missatgeContenedor .horaMissatge {
  display: flex;
  justify-content: flex-end;
}

.missatgeContenedor::-webkit-scrollbar {
  width: 10px;
}

.missatgeContenedor::-webkit-scrollbar-thumb {
  background-color: #ccc;
  border-radius: 5px;
}

.missatgeContenedor::-webkit-scrollbar-track {
  background-color: #f1f1f1;
  border-radius: 5px;
}

.missatgeContenedor::-webkit-scrollbar-thumb:hover {
  background-color: #aaa;
}

.missatge {
  width: auto;
  margin: 3px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
  word-wrap: break-word;
  display: flex;
  flex-direction: column;
  gap: 5px;
}

select {
  margin: 10px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

select:hover {
  cursor: pointer;
}
</style>
