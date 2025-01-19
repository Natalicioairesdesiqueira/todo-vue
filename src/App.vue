<script setup>
import { reactive } from 'vue';

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
  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>MINHAS TAREFAS</h1>
    <p>
      voce possui {{ getTarefasPendentes().length }} tarefas pendentes
    </p>
  </header>
  <form @submit.prevent="cadastraTarefa">
  <div class="row">
    <div class="col">
      <input :value="estado.tarefadigi" @change="evento => estado.tarefadigi = evento.target.value" required type="text" placeholder="Adicione uma tarefa" class="form-control">
    </div>
    <div class="col-md-2">
      <button type="submit" class="btn btn-primary">CADASTRAR</button>
    </div>
    <div class="col-md-2">
      <select @change="evento => estado.filtro = evento.target.value" class="form-control">
        <option value="todas">TODAS TAREFAS</option>
        <option value="pendentes">PENDENTES</option>
        <option value="finalizadas">FINALIZADAS</option>
      </select>
    </div>
  </div>
</form>
<ul class="list-group mt-4">
  <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
    <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
    <label :class="{ done: tarefa.finalizada  }" class="ms-3" :for="tarefa.titulo">
      {{ tarefa.titulo }}
    </label>
  </li>
</ul>
</div>

</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
