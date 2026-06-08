<script setup>
  // Props: configuram só a APARÊNCIA e o TEXTO. Nenhuma regra de negócio aqui.
  const props = defineProps({
    texto: String,   // o que aparece escrito no botão
    cor: String      // cor de fundo
  })

  // defineEmits declara os eventos que este componente pode AVISAR ao pai.
  // É uma macro do <script setup>, não precisa importar.
  // Aqui só existe "clicar": o botão não sabe O QUE será feito, só avisa o clique.
  const emit = defineEmits(['clicar'])
</script>

<template>
  <!-- Ao clicar, o botão apenas emite o evento. A decisão fica com o pai. -->
  <button class="botao" :style="{ backgroundColor: cor }" @click="emit('clicar')">
    {{ texto }}
  </button>
</template>

<style scoped>
  .botao {
    border: none;
    color: #fff;
    padding: 8px 16px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 14px;
    margin-right: 8px;
  }
</style>
