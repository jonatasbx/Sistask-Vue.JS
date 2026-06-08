<script setup>
  import { ref } from 'vue'
  import Botao from './Botao.vue'

  const props = defineProps({
    title: String,
    color: String
  })

  const tarefas = ref([
    { id: 1, texto: 'Estudar watchers', feita: false },
    { id: 2, texto: 'Montar o layout', feita: false }
  ])

  // NOVO: guarda o texto que está sendo digitado no campo.
  const novaTarefa = ref('')

  function adicionarTarefa() {
    // Ignora se o campo estiver vazio (ou só com espaços).
    if (novaTarefa.value.trim() === '') return

    tarefas.value.push({
      id: Date.now(),
      texto: novaTarefa.value,   // usa o texto digitado, não mais um texto fixo
      feita: false
    })

    novaTarefa.value = ''   // limpa o campo depois de adicionar
  }

  function limparTudo() {
    tarefas.value = []
  }

  function alternarFeita(tarefa) {
    tarefa.feita = !tarefa.feita
  }

  function removerTarefa(id) {
    tarefas.value = tarefas.value.filter(t => t.id !== id)
  }
</script>

<template>
  <section class="lista">
    <h2 :style="{ color: color }">{{ title }}</h2>

    <!-- NOVO: campo ligado por v-model à ref novaTarefa. -->
    <!-- @keyup.enter também adiciona ao apertar Enter (modifier de tecla, que você já viu). -->
    <input
      v-model="novaTarefa"
      @keyup.enter="adicionarTarefa"
      type="text"
      placeholder="Digite o nome da tarefa"
      class="campo"
    >

    <ul>
      <li v-for="tarefa in tarefas" :key="tarefa.id" class="item">
        <span :class="{ feita: tarefa.feita }">{{ tarefa.texto }}</span>
        <div class="acoes">
          <button @click="alternarFeita(tarefa)">✓</button>
          <button @click="removerTarefa(tarefa.id)">🗑</button>
        </div>
      </li>
    </ul>

    <div class="botoes">
      <Botao texto="Adicionar" cor="#1D9E75" @clicar="adicionarTarefa" />
      <Botao texto="Limpar tudo" cor="#D85A30" @clicar="limparTudo" />
    </div>
  </section>
</template>

<style scoped>
  .lista { padding: 16px; }
  .campo {
    width: 100%;
    padding: 8px;
    margin-bottom: 12px;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-sizing: border-box;
  }
  .item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
    border-bottom: 1px solid #eee;
  }
  .feita {
    text-decoration: line-through;
    opacity: 0.5;
  }
  .acoes button {
    border: none;
    background: transparent;
    cursor: pointer;
    font-size: 16px;
    margin-left: 8px;
  }
  .botoes { margin-top: 16px; }
</style>
