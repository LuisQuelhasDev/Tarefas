<script setup>
    const props = defineProps(["tarefasPendentes"])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Tarefas</h1>
            <p>
                {{ props.tarefasPendentes }} tarefas pendentes
            </p>
    </header>
</template>