<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar Ajax',
        finalizada: false,
      },
      {
        titulo: 'Estudar CSS',
        finalizada: true,
      },
    ],
    filtro: 'todas',
    novaTarefaTemp: '',
  })

  const getTarefasPendentes = () => {
      return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  } 

  const getTarefasFinalizadas = () => {
      return estado.tarefas.filter(tarefa => tarefa.finalizada)
  } 

  const getTarefasFiltradas = () =>{
    const {filtro} = estado;

    switch (filtro){
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
      return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const novaTarefa = {
      titulo: estado.novaTarefaTemp,
      finalizada: false
    }
    estado.tarefas.push(novaTarefa)
    estado.novaTarefaTemp = ''
  }



</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{getTarefasPendentes().length}} Tarefas Pendentes
      </p>
    </header>
  </div>
  <div class="container">
    <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input :value="estado.novaTarefaTemp" @change="e => estado.novaTarefaTemp = e.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select class="form-control" @change="e => estado.filtro = e.target.value">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="e => tarefa.finalizada = e.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" >
        <label class="ms-3" :for="tarefa.titulo" :class="{done: tarefa.finalizada}">{{tarefa.titulo}}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
