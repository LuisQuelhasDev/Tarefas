<script setup>
    const props = defineProps(["tarefas"])
</script>

<template>
    <div>
        <p v-if="props.tarefas.length === 0" class="mt-2">Nenhuma tarefa está pendente!</p>

        <ul v-else class="ul list-group mt-4">
            <li class="li list-group-item" v-for = "tarefa in props.tarefas">
                <input 
                    @change="evento => tarefa.finalizada = evento.target.checked" 
                    :checked = "tarefa.finalizada" 
                    :id="tarefa.titulo" type="checkbox">
                <label 
                    :class="{done: tarefa.finalizada}" 
                    class="ms-3" :for="tarefa.titulo">{{tarefa.titulo}}
                </label>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>