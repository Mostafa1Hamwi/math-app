<script setup>
import OperatorSelector from "./OperatorSelector.vue";
import OperatorQuiz from "./OperatorQuiz.vue";
import { ref } from "vue";
const operator = ref("");
function selectOperator(sign) {
  operator.value = sign;
}

function clearOperator() {
  operator.value = null;
}
</script>

<template>
  <div class="min-h-screen flex flex-col items-center justify-center gap-6">
    <h1 class="text-5xl font-bold text-black">Welcome To The Math Quiz App</h1>
    <h2 v-if="!operator" class="text-3xl font-bold text-gray-800">
      Choose an operation
    </h2>
    <OperatorSelector v-if="!operator" @selectOperator="selectOperator" />
    <OperatorQuiz
      @onBack="clearOperator"
      v-if="operator"
      :operator="operator"
    />
  </div>
</template>
