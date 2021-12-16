<template>
  <div class="action-buttons">
          <button 
            class="btn" 
            v-if="activeStep < formSteps.length" 
            @click.prevent="prevStep"
            :disabled="prevDisabled"
          >Назад</button>
          <button 
            class="btn" 
            v-if="activeStep +1 < formSteps.length" 
            @click.prevent="validateFields"
          >Вперед</button>
          <button 
            class="btn" 
            v-if="activeStep +1 === formSteps.length" 
            @click="resetForm"
          >Начать заново</button>
        </div>
</template>

<script>
export default {
  name: 'FormButtons',
  props: {
    activeStep: Number,
    formSteps: Array,
  },
  methods: {
    prevStep() {
      this.$emit('prev');
    },
    validateFields() {
      this.$emit('validate');
    },
    resetForm() {
      this.$emit('reset');
    },
    nextStep() {
      this.$emit('next');
    },
  },
  computed: {
    prevDisabled() {
      return this.activeStep === 0
    },
  },
}
</script>