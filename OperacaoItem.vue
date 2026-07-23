<template>
    <li class="operacao-item">
      <span>{{ numero1 }} {{ simboloExibicao }} {{ numero2 }} = <strong>{{ resultado }}</strong></span>
    </li>
  </template>
  
  <script setup>
  import { computed } from 'vue'
  
  // Define as propriedades que o componente pai vai passar
  const props = defineProps({
    numero1: {
      type: Number,
      required: true
    },
    numero2: {
      type: Number,
      required: true
    },
    operacao: {
      type: String,
      required: true
    }
  })
  
  // Altera o símbolo interno (+, -, *, /) para uma exibição mais amigável (x, ÷)
  const simboloExibicao = computed(() => {
    switch (props.operacao) {
      case '*': return 'x'
      case '/': return '÷'
      default: return props.operacao
    }
  })
  
  // Realiza o cálculo aritmético com base na operação recebida
  const resultado = computed(() => {
    const n1 = props.numero1
    const n2 = props.numero2
  
    switch (props.operacao) {
      case '+': return n1 + n2
      case '-': return n1 - n2
      case '*': return n1 * n2
      case '/': return n2 !== 0 ? n1 / n2 : 'Erro (Divisão por 0)'
      default: return 0
    }
  })
  </script>
  
  <style scoped>
  .operacao-item {
    padding: 8px;
    background-color: #f4f4f5;
    margin-bottom: 5px;
    border-radius: 4px;
    list-style-type: square;
    font-family: monospace;
    font-size: 1.1rem;
  }
  strong {
    color: #42b883;
  }
  </style>
  