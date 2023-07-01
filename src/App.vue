<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    tarefas: [
      {
        id: 1,
        titulo: 'Estudar ES6',
        finalizada: false
      },
      {
        id: 2,
        titulo: 'Estudar SASS',
        finalizada: false
      },
      {
        id: 3,
        titulo: 'Estudar VUE',
        finalizada: true
      }
    ],
    filtro: 'todas',
    newTask: ''
  })

  const getTasksPendentes = () => {
    return estado.tarefas.filter(item => !item.finalizada)
  }

  const getTasksFinalizadas = () => {
    return estado.tarefas.filter(item => item.finalizada)
  }

  const getTasksFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {

      case 'pendentes':
        return getTasksPendentes();

      case 'finalizadas':
        return getTasksFinalizadas();

      default: 
        return estado.tarefas;

    }
  }

  const addTask = () => {
    const { tarefas, newTask } = estado;
    if (newTask == '') {
      alert('Digite a tarefa.');
    }else {
      const tarefaNova = {
        id: tarefas.length + 1,
        titulo: estado.newTask,
        finalizada: false
      }
      tarefas.push(tarefaNova);
      estado.newTask = '';
    }

  }

</script>

<template>
  <div class="container">

    <Cabecalho :tarefas-pendentes="getTasksPendentes().length" />
    <Formulario :filtro="evento => estado.filtro = evento.target.value" :add-task="addTask" :edita-new-task="evento => estado.newTask = evento.target.value" :new-task="estado.newTask" />
    <ListaDeTarefas :tarefas="getTasksFiltradas()" />
    
  </div>
</template>
