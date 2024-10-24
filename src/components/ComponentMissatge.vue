<script setup>
import { defineProps, defineEmits, ref } from 'vue'
const props = defineProps(['autor', 'onNouMissatge'])
const emits = defineEmits(['onNouMissatge'])

let missatge = ref('')

const onSubmit = () => {
  //console.log(missatge)
  emits('onNouMissatge', { missatge: missatge.value, usuari: props.autor })
  missatge.value = ''
}
</script>

<template>
  <form v-on:submit.prevent="onSubmit()">
    <input type="text" placeholder="Missatge" v-model="missatge" required />
    <button>Enviar</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  margin: 10px;
}

input {
  padding: 5px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 5px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
}

button:hover {
  background-color: #0056b3;
  cursor: pointer;
}
</style>
