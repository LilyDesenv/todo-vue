<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue'
  import Formulario from './components/Formulario.vue'
  import ListaDeTarefas from './components/ListaDeTarefas.vue'

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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario  :nova-tarefa-temp="estado.novaTarefaTemp" :editaNovaTarefaTemp="e => estado.novaTarefaTemp = e.target.value" :cadastraTarefa="cadastraTarefa" :trocarFiltro="e => estado.filtro = e.target.value"/>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
    
  </div>
</template>

