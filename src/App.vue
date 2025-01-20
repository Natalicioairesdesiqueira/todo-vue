<script setup>
import { reactive } from 'vue';

import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive ({
  filtro: 'todas',
  tarefadigi: '',
  tarefas: [
    {
      titulo: 'Estudar para o exame',
      finalizada: false,
    },
    {
      titulo: 'Estudar sass',
      finalizada: false,
    },
    {
      titulo: 'ir para academia',
      finalizada: true,
    },
  ],
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefas => !tarefas.finalizada)
}
const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefas => tarefas.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;  
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefadigi,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefadigi = '';
}

</script>

<template>
<div class="container">
  <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
  <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefadigi="estado.tarefadigi" :edita-tarefadigi="evento => estado.tarefadigi = evento.target.value" :cadastra-tarefa="cadastraTarefa"/>
  <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  

</div>

</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
