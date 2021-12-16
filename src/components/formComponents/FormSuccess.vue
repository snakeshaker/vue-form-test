<template>
  <div 
    v-if="activeStep +1 === formSteps.length"
    class="final-info"
  >
    <p> <span>Ваше имя:</span> {{ formInfo.name }}</p>
    <p><span>Ваша почта:</span> {{ formInfo.email }}</p>
    <p><span>Ваш номер телефона:</span> {{ formInfo.phoneNumber }}</p>
    <p class="final-info-center">Форма заполнена успешно!</p>
  </div>
</template>

<script>
export default {
  name: 'FormSuccess',
  props: {
    activeStep: Number,
    formSteps: Array,
    formInfo: Object,
  }
}
</script>