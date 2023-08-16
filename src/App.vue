<script setup>
import { reactive, ref, watch } from 'vue';

const estado = reactive({
  filtro: 'adicao', 
  operando1: '',
  operando2: '',
  resultado: '',
});

const calcular = () => {
  switch (estado.filtro) {
    case 'adicao':
      estado.resultado = estado.operando1 + estado.operando2;
      break;
    case 'subtracao':
      estado.resultado = estado.operando1 - estado.operando2;
      break;
    case 'multiplicacao':
      estado.resultado = estado.operando1 * estado.operando2;
      break;
    case 'divisao':
      if (estado.operando2 !== 0) {
        estado.resultado = estado.operando1 / estado.operando2;
      } else {
        estado.resultado = 'Divisão por zero não é definida';
      }
      break;
    default:
      estado.resultado = 'Operação inválida';
  }
};

watch([estado.operando1, estado.operando2], () => {
  calcular();
});

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-primary rounded-3">
      <h1>Calculadora aritmética</h1>
    </header>
    <form>
      <div class="row">
        <div id="campo" class="col-2">
          <select v-model="estado.filtro" class="form-control mt-3 mb-3 text-end">
            <option value="adicao">+ Adição</option>
            <option value="subtracao">- Subtração</option>
            <option value="divisao">/ Divisão</option>
            <option value="multiplicacao">* Multiplicação</option>
          </select>
          <input v-model.number="estado.operando1" type="numeric" placeholder="0" class="form-control mt-3 mb-3 text-end">
          <input v-model.number="estado.operando2" type="numeric" placeholder="0" class="form-control mt-3 mb-3 text-end">
        </div>
        <div class="mt-3">
          <button @click="calcular" type="button" class="btn btn-primary mb-3">Calcular</button>
        </div>
      </div>
    </form>
    <span class="pd-5"><h3>Resultado: {{ estado.resultado }}</h3></span>
  </div>
</template>
<style scoped>
header h1 {
  color: #fff;
}
</style>
