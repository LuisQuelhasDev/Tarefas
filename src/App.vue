<script setup>
import {reactive} from "vue";

  const estado = reactive({
    filtro:"todas",
    tarefaTemp: "",
    tarefas:[
      {
        titulo: "Estudar ES6",
        finalizada: false,
      },
      {
        titulo: "Estudas Sass",
        finalizada: false,
      },
      {
        titulo:"Estudar Css",
        finalizada: true,
      }
    ]
  })

  const getTarefaPendentes = () =>{
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefaFinalizada = () =>{
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefaFiltrada = () => {
    const {filtro} = estado;

    switch (filtro) {
      case "pendentes":
        return getTarefaPendentes();
      case "finalizadas":
        return getTarefaFinalizada();
      default:
        return estado.tarefas;
    }
  } 

  const cadastraTarefa = () =>{
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = "";
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Tarefas</h1>
      <p>
        {{ getTarefaPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required class="form-control" type="text" placeholder="Digite a descrição da tarefa">
        </div>
        <div class="col-md-1">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change ="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas as Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="ul list-group mt-4">
      <li class="li list-group-item" v-for = "tarefa in getTarefaFiltrada()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked = "tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">{{tarefa.titulo}}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
