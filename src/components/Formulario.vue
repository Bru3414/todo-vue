<script setup>
    const props = defineProps(['addTask', 'newTask', 'filtro', 'editaNewTask']);
</script>

<template>
    <form @submit.prevent="props.addTask">
        <div class="row">
            <div class="col">
                <input :value="props.newTask" @change="props.editaNewTask" class="form-control"
                    type="text" placeholder="Digite a descrição da tarefa" required>
            </div>
            <div class="col-md-2">
                <button @click="addTask" type="button" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.filtro" class="form-control">
                    <option selected value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendêntes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>