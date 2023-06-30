<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListadeTarefas from './components/ListaDeTarefas.vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Finalizar projeto',
      finalizada: true
    },
    {
      titulo: 'Descansar',
      finalizada: true
    }

  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
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
    titulo: estado.tarefaTemp,
    finalizada: false,
  }

  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}


</script>

<template>
  <div class="container">

    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :valor-tarefa-temp="estado.tarefaTemp"
      :envia-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-nova-tarefa="cadastraTarefa"
      :captura-filtro="evento => estado.filtro = evento.target.value"/>
    <ListadeTarefas :tarefas-filtradas="getTarefasFiltradas()" />



  </div>
</template>

<style scoped>

</style>
