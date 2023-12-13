<script setup>
import Operation from "./Operation.vue";
</script>
<template>
  <div class="flex gap-5 items-center justify-center mt-10">
    <Operation @click="$emit('selectOperator', '+')">
      Addition <br />
      (+)
    </Operation>
    <Operation @click="$emit('selectOperator', '-')"
      >Substraction <br />
      (-)</Operation
    >
    <Operation @click="$emit('selectOperator', '*')"
      >Multiplication <br />
      (*)</Operation
    >
    <Operation @click="$emit('selectOperator', '/')"
      >Division <br />
      (/)</Operation
    >
  </div>
</template>
