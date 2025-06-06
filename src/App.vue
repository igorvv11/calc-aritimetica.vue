<script setup>
import { reactive, computed } from 'vue'

const estado = reactive({
  aritimetica: 'soma',
  resultado: 0,
  valorA: 0,
  valorB: 0
})

const simboloOperacao = computed(() => {
  switch (estado.aritimetica) {
    case 'soma': return '+'
    case 'subtrair': return '−'
    case 'multiplicar': return '×'
    case 'dividir': return '÷'
    default: return '?'
  }
})

function somar(a, b) {
  return estado.resultado = a + b
}
function subtrai(a, b) {
  return estado.resultado = a - b
}
function multiplica(a, b) {
  return estado.resultado = a * b
}
function divide(a, b) {
  return estado.resultado = a / b
}

const recebeValorA = evento => {
  estado.valorA = Number(evento.target.value)
  EscolhaAritimetica()
}
const recebeValorB = evento => {
  estado.valorB = Number(evento.target.value)
  EscolhaAritimetica()
}

const EscolhaAritimetica = () => {
  const { aritimetica, valorA, valorB } = estado;

  switch (aritimetica) {
    case 'soma':
      return somar(valorA, valorB)

    case 'subtrair':
      return subtrai(valorA, valorB)

    case 'multiplicar':
      return multiplica(valorA, valorB)

    case 'dividir':
      return divide(valorA, valorB)
  }
}
</script>

<template>
  <div class="container">
    <header class="bg-light py-3">
      <h1 class="text-center">Calculadora</h1>
    </header>

    <div class="row justify-content-center mt-5">
      <div class="col-3">
        <input @change="recebeValorA" class="form-control" type="number" placeholder="Digite um número">
      </div>
      <div class="col-1 text-center">
        <span class="fs-4">{{ simboloOperacao }}</span>
      </div>
      <div class="col-3">
        <input @change="recebeValorB" class="form-control" type="number" placeholder="Digite outro número">
      </div>
      <div class="col-2">
        <select @change="e => { estado.aritimetica = e.target.value; EscolhaAritimetica(); }" class="form-control">
          <option value="soma">Somar +</option>
          <option value="subtrair">Subtrair -</option>
          <option value="multiplicar">Multiplicar ×</option>
          <option value="dividir">Dividir ÷</option>
        </select>
      </div>
    </div>

    <div class="row justify-content-center mt-4">
      <div class="col-auto">
        <h3 class="text-success">Resultado: {{ estado.resultado }}</h3>
      </div>
    </div>
  </div>
</template>
