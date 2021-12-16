<template>
   <div class="input-fields">
      <div 
         class="input-container"
         v-for="(field, index) in formSteps[activeStep].fields"
         :key="index"
      >
         <label class="input-label">{{ field.label }}</label>
         <label v-if="!field.valid" class="input-label-err">{{ field.err }}</label>
         <input 
            v-if="activeStep !== 1"
            type="text" 
            :class="{'wrong-input': !field.valid}" 
            v-model="field.value" 
            required
            :placeholder="field.err"
         >
         <span
            v-if="activeStep === 1"
            class="input-num"
         >+7</span>
         <input
            v-if="activeStep === 1"
            type="tel" 
            :class="{'wrong-input': !field.valid}"
            v-model="field.value"
            placeholder="(xxx) xxx-xxxx"
            autocomplete="tel"
            maxlength="14"
            v-phone
            required
         />
      </div>
   </div>
</template>

<script>
export default {
   name: 'FormInputs',
   props: {
      activeStep: Number,
      formSteps: Array,
   },
   directives: {
      phone: {
         beforeMount(el) {  
         el.oninput = function(e) {
               if (!e.isTrusted) {
                  return;
               }
         
               const x = this.value.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
               this.value = !x[2] ? x[1] : '(' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : '');
               el.dispatchEvent(new Event('input'));
            }
         },
      }
   }
}
</script>