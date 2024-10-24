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
  //console.log(missatge)
  missatges.value.push(missatge)
}
</script>

<template>
  <div class="container">
    <!-- escollir un usuari -->
    <select v-model="autor" v-on:change="console.log(autor)">
      <option value="Pere">Pere</option>
      <option value="Joan">Joan</option>
    </select>

    <div class="missatge" v-for="missatge in missatges" :key="missatge.idMissatge">
      <strong>{{ missatge.usuari }}:</strong> {{ missatge.missatge }}
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

.missatge {
  width: auto;
  padding: 10px;
  margin: 2px 10px 2px 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
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
