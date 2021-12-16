<template>
   <header>
      <h1>Тестовое задание формы</h1>
      <ul class="steps-list">
         <li 
            class="steps-item"
            :class="{
               'active': index === activeStep,
               'done': index < activeStep
            }"
            v-for="(step, index) in formSteps"
            :key="index"
         >
            <span>
               {{ index + 1 }}
            </span>
         </li>
      </ul>
   </header>
</template>

<script>
export default {
   name: 'FormHeader',
   props: {
      activeStep: Number,
      formSteps: Array,
   }
}
</script>