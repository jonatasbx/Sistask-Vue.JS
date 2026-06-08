<script setup>
  import { ref } from 'vue'
  import Navbar from './components/Navbar.vue'
  import Lista from './components/Lista.vue'

  // O estado do menu MORA AQUI, pois ele controla o layout de tudo abaixo:
  // a coluna do menu e o conteúdo precisam reagir juntos a ele.
  const menuAberto = ref(false)

  function alternarMenu() {
    menuAberto.value = !menuAberto.value
  }
</script>

<template>
  <!-- A Navbar só avisa o clique com o evento 'alternar'. O App decide o resto. -->
  <Navbar title="Minhas Tarefas" color="#1D9E75" @alternar="alternarMenu" />

  <!-- Corpo em duas colunas: menu à esquerda, conteúdo à direita. -->
  <div class="corpo">
    <!-- Coluna da esquerda: aparece só quando o menu está aberto. -->
    <aside class="menu-lateral" v-show="menuAberto">
      <ul>
        <li>Início</li>
        <li>Tarefas</li>
        <li>Sobre</li>
      </ul>
    </aside>

    <!-- Conteúdo: ocupa o espaço restante e recua para a direita ao abrir o menu. -->
    <main class="conteudo">
      <Lista title="Lista de hoje" color="#534AB7" />
    </main>
  </div>
</template>

<style scoped>
  .corpo {
    display: flex;          /* coloca menu e conteúdo lado a lado */
    align-items: stretch;   /* o menu estica por toda a altura da coluna */
  }
  .menu-lateral {
    width: 200px;           /* a coluna da esquerda */
    background: #1D9E75;
    padding: 16px;
    color: white;
    border-radius: 0px 0px 5px 5px;
  }
  .menu-lateral ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  .menu-lateral li {
    padding: 8px 0;
    cursor: pointer;
  }
  .conteudo {
    flex: 1;                /* ocupa o resto: ao abrir o menu, é empurrado p/ direita */
  }
</style>
