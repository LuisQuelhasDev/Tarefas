<script setup>
import {reactive} from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue";
import Lista from "./components/Lista.vue";

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
        finalizada: false,
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
    <Cabecalho :tarefas-pendentes="getTarefaPendentes().length"/>
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" 
      :edita-tarefa="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <Lista :tarefas="getTarefaFiltrada()" />
  </div>
</template>


