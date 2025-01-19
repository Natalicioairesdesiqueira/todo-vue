<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas Tarefas</h1>
        <h5>Exercício prático sobre Vue JS Módulo 27 - Curso EBAC</h5>
        <p>
            Você possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>