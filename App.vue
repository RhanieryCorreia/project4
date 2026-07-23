<template>
  <div class="calculadora-contentor">
    <h2>Histórico de Operações</h2>

    <!-- Inputs para os números -->
    <div class="inputs-grupo">
      <input 
        v-model.number="num1" 
        type="number" 
        placeholder="Número 1" 
      />
      <input 
        v-model.number="num2" 
        type="number" 
        placeholder="Número 2" 
      />
    </div>

    <!-- Botões das operações aritméticas -->
    <div class="botoes-grupo">
      <button @click="adicionarConta('+')">+</button>
      <button @click="adicionarConta('-')">-</button>
      <button @click="adicionarConta('*')">x</button>
      <button @click="adicionarConta('/')">÷</button>
    </div>

    <!-- Lista não-ordenada que exibe o histórico -->
    <div class="lista-resultados">
      <h3>Resultados:</h3>
      <p v-if="historicoContas.length === 0">Nenhuma operação realizada ainda.</p>
      
      <ul>
        <!-- Instanciação do componente filho enviando os dados necessários via props -->
        <OperacaoItem 
          v-for="item in historicoContas" 
          :key="item.id"
          :numero1="item.n1"
          :numero2="item.n2"
          :operacao="item.op"
        />
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import OperacaoItem from './components/OperacaoItem.vue'

// Estados reativos para os inputs
const num1 = ref(0)
const num2 = ref(0)

// Vetor (array) que irá armazenar o histórico de contas feitas
const historicoContas = ref([])

// Função executada ao clicar em qualquer um dos 4 botões
function adicionarConta(simbolo) {
  // Validação básica para garantir que campos vazios não quebrem a lógica
  if (num1.value === null || num2.value === null) return

  // Adiciona um novo objeto de conta ao vetor histórico
  historicoContas.value.push({
    id: Date.now(), // ID único baseado no timestamp atual
    n1: num1.value,
    n2: num2.value,
    op: simbolo
  })
}
</script>

<style scoped>
.calculadora-contentor {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-family: sans-serif;
}
.inputs-grupo {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
}
.inputs-grupo input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.botoes-grupo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
.botoes-grupo button {
  flex: 1;
  padding: 10px;
  background-color: #35495e;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1.2rem;
  font-weight: bold;
}
.botoes-grupo button:hover {
  background-color: #42b883;
}
.lista-resultados h3 {
  margin-top: 0;
  border-bottom: 2px solid #eee;
  padding-bottom: 5px;
}
ul {
  padding-left: 20px;
}
</style>