<script setup>
  import { reactive } from 'vue';

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
    const { tarefas } = estado;

    const tarefaNova = {
      id: tarefas.length + 1,
      titulo: estado.newTask,
      finalizada: false
    }

    tarefas.push(tarefaNova);
    estado.newTask = '';
  }

</script>

<template>
  <div class="container">
    <header class="p-5 mt-4 mb-4 rounded-3 bg-light">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTasksPendentes().length }} tarefas pendêntes</p>
    </header>
    <form @submit.prevent="addTask">
      <div class="row">
        <div class="col">
          <input :value="estado.newTask" @change="evento => estado.newTask = evento.target.value" class="form-control" type="text" placeholder="Digite a descrição da tarefa" required>
        </div>
        <div class="col-md-2">
          <button @click="addTask" type="button" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option selected value="todas">Todas as tarefas</option>
            <option value="pendentes">Pendêntes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTasksFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" v-bind:checked="tarefa.finalizada" :id="tarefa.id" type="checkbox">
        <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.id">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
