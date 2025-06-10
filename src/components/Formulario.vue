<script setup>
    const props = defineProps(["cadastraTarefa", "tarefaTemp", "trocarFiltro", "editaTarefa"])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefa" required class="form-control" type="text" placeholder="Digite a descrição da tarefa">
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change ="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas as Tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>