<script setup>
    const props = defineProps(['tarefas'])
</script>
<template>
    <ul class="list-group mt-4" v-if="props.tarefas.length > 0">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" >
            <label class="ms-3" :for="tarefa.titulo" :class="{done: tarefa.finalizada}">{{tarefa.titulo}}</label>
        </li>
    </ul>
    <h5 v-else class="mt-3">Não há Tarefas!</h5>
</template>
<style scoped>
    .done{
        text-decoration: line-through;
    }
</style>
