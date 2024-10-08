<script setup>
  import {reactive} from 'vue';
  import Cabecalho from './components/cabecalho.vue'
  import Formulario from './components/Formulario.vue'
  import ListaDeTarefas from './components/ListaDeTarefas.vue'


 const reativos = reactive({
    filtro: 'todas',
    tarefaInput: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada:false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada:false,
      },
      {
        titulo: 'Estudar VueJS',
        finalizada:true,
      }
    ]

 });

 const getTarefasPendentes = () => {
  return reativos.tarefas.filter(tarefa => tarefa.finalizada === false)
 }

 const getTarefasFinalizadas = () => {
  return reativos.tarefas.filter(tarefa => tarefa.finalizada === true)
 }

 const getTarefasFiltradas = () => {
    const filtro = reativos.filtro;
    switch (filtro){
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return reativos.tarefas;
    } 
 }

 const cadastrarTarefa = () => {
  const novaTarefa = {
    titulo: reativos.tarefaInput,
    finalizada: false
  }
  reativos.tarefas.push(novaTarefa);
  reativos.tarefaInput = '';
 }

</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"></Cabecalho>
    <Formulario :trocar-filtro="evento => reativos.filtro = evento.target.value" :tarefa-input="reativos.tarefaInput" :editar-tarefa-input="evento => reativos.tarefaInput = evento.target.value" :cadastrar-tarefa="cadastrarTarefa"></Formulario>
    <ListaDeTarefas :tarefas="getTarefasFiltradas()"></ListaDeTarefas>
  </div>

</template>
