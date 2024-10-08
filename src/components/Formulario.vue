<script setup>
    const props = defineProps([
        'cadastrarTarefa', 'tarefaInput', 'trocarFiltro', 'editarTarefaInput'
    ])
</script>
<template>
    <form @submit.prevent="props.cadastrarTarefa" action="">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaInput" @change="props.editarTarefaInput"
                    class="form-control" type="text" placeholder="Digite a descrição da tarefa">
            </div>
            <div class="col-1 me-3">
                <button class='btn btn-primary'>Cadastrar </button>
            </div>
            <div class="col-2">
                <select @change="props.trocarFiltro" class="form-control" name="" id="">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>