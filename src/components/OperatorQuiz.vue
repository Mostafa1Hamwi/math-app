<script setup>
import { ref } from "vue";
import Operation from "./Operation.vue";

const props = defineProps(["operator"]);
const operandLeft = ref("");
const operandRight = ref("");
const QuizStarted = ref(false);
const answers = ref([]);
const expectedAnswer = ref("");
const rightAnswer = ref(false);

function selectAnswer(answer) {
  if (answer === expectedAnswer.value) {
    rightAnswer.value = true;
  } else {
    alert("Wrong answer");
    rightAnswer.value = false;
    startQuiz();
  }
}

function startQuiz() {
  const operator = props.operator;
  operandLeft.value = parseInt(Math.random() * 13);
  operandRight.value = parseInt(Math.random() * 13);
  QuizStarted.value = true;
  const methods = {
    "+": (a, b) => a + b,
    "-": (a, b) => a - b,
    "*": (a, b) => a * b,
    "/": (a, b) => a / b,
  };

  const methodToUse = methods[operator];
  answers.value = [];

  answers.value.push(methodToUse(operandLeft.value, operandRight.value + 1));
  answers.value.push(
    methodToUse(operandLeft.value + 1, operandRight.value + 1)
  );
  answers.value.push(
    methodToUse(operandLeft.value - 1, operandRight.value + 1)
  );
  answers.value.push(methodToUse(operandLeft.value, operandRight.value - 1));
  answers.value.push(
    methodToUse(operandLeft.value + 1, operandRight.value - 1)
  );

  const correctAnswer = methodToUse(operandLeft.value, operandRight.value);
  answers.value[parseInt(Math.random() * answers.value.length)] = correctAnswer;

  expectedAnswer.value = correctAnswer;
}
</script>
<template>
  <div class="flex gap-10 mt-10">
    <button
      class="bg-red-600 text-xl text-white py-2 px-4 rounded-md hover:bg-red-700"
      @click="$emit('onBack')"
    >
      Back
    </button>
    <Operation v-if="!QuizStarted" @click="startQuiz"> Start Quiz </Operation>
  </div>
  <h2 class="text-3xl text-green-600 font-bold" v-if="rightAnswer">
    Congrats! You got it right
  </h2>
  <div v-if="QuizStarted">
    <div
      class="flex justify-center bg-gray-700 border-black border-4 rounded-md"
    >
      <h4 class="text-2xl text-white py-2">
        {{ operandLeft }} {{ operator }} {{ operandRight }}
      </h4>
    </div>
    <div class="flex gap-5 mt-10 justify-center items-center">
      <button
        @click="selectAnswer(answer)"
        class="bg-blue-600 text-xl py-1 px-2 rounded-md text-white w-12 hover:bg-blue-700"
        v-for="answer in answers"
        :key="answer"
      >
        {{ answer }}
      </button>
    </div>
  </div>
</template>
