<script setup>
    const props = defineProps(['cadastraNovaTarefa','valorTarefaTemp', 'enviaTarefaTemp', 'capturaFiltro'])
</script>

<template>
    <form @submit.prevent="props.cadastraNovaTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.valorTarefaTemp" @change="props.enviaTarefaTemp" required
                    type="text" class="form-control" placeholder="Digite aqui a descrição da tarefa">
            </div>

            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            
            <div class="col-md-2">
                <select @change="props.capturaFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>