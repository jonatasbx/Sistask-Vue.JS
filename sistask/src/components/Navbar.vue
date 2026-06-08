<script setup>
  const props = defineProps({
    title: String,
    color: String
  })

  // A Navbar não guarda mais o estado: só AVISA o clique para o App.
  const emit = defineEmits(['alternar'])
</script>

<template>
  <nav class="navbar" :style="{ backgroundColor: color }">
    <!-- Botão do menu agora à ESQUERDA (primeiro item do flex) -->
    <button class="botao-menu" @click="emit('alternar')">☰</button>
    <span>{{ title }}</span>
  </nav>
</template>

<style scoped>
  .navbar {
    display: flex;
    align-items: center;
    gap: 12px;            /* espaço entre o botão e o título */
    padding: 12px 16px;
    color: #fff;
    border-radius:8px 8px 8px 0px ;
  }
  .botao-menu {
    background: transparent;
    border: none;
    color: #fff;
    font-size: 20px;
    cursor: pointer;
  }
</style>
