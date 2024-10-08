<script setup>
import {reactive} from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>

    <form @submit.prevent="cadastrarTarefa" action="">
    <div class="row">
      <div class="col">
        <input :value="reativos.tarefaInput" @change="evento => reativos.tarefaInput = evento.target.value" class="form-control" type="text" placeholder="Digite a descrição da tarefa">
      </div>
      <div class="col-1 me-3">
        <button class='btn btn-primary'>Cadastrar </button>
      </div>
      <div class="col-2">
        <select @change=" evento => reativos.filtro = evento.target.value" class="form-control" name="" id="">
          <option value="todas">Todas as tarefas</option>
          <option value="pendentes">Tarefas pendentes</option>
          <option value="finalizadas">Tarefas finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li v-for="tarefa in getTarefasFiltradas()" class="list-group-item">
      <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo"  type="checkbox">
      <label :class="{done: tarefa.finalizada === true}" class="ms-3" :for="tarefa.titulo">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
  </div>

</template>

<style scoped>
.done{
  text-decoration:line-through;
}
</style>
