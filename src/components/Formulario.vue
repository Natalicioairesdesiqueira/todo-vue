<script setup>
const props = defineProps(['cadastraTarefa', 'tarefadigi', 'trocarFiltro', 'editaTarefadigi'])
</script>
<template>
<form @submit.prevent="props.cadastraTarefa">
    <div class="row">
        <div class="col">
            <input :value="props.tarefadigi" @change="props.editaTarefadigi" required
                type="text" placeholder="Qual é a sua tarefa?" class="form-control">
        </div>
        <div class="col-md-2">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
            <select @change="props.trocarFiltro" class="form-control">
                <option value="todas">Todas as Tarefas</option>
                <option value="pendentes">Pendentes</option>
                <option value="finalizadas">Finalizadas</option>
            </select>
        </div>
    </div>
</form>
</template>