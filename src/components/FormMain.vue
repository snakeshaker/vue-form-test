<template>
   <form class="card form-control">
      <form-header
         :activeStep="activeStep"
         :formSteps="formSteps"
      />
      <section>
         <h2>{{ formSteps[activeStep].title }}</h2>
         <form-inputs
            :activeStep="activeStep"
            :formSteps="formSteps"
         />
         <form-success
            :activeStep="activeStep"
            :formSteps="formSteps"
            :formInfo="formInfo"
         />
         <form-buttons 
            :activeStep="activeStep"
            :formSteps="formSteps"
            @prev="prevStep"
            @next="nextStep"
            @validate="validateFields"
            @reset="resetForm"
         />
      </section>
    </form>
</template>

<script>
import FormButtons from './formComponents/FormButtons.vue';
import FormInputs from './formComponents/FormInputs.vue';
import FormSuccess from './formComponents/FormSuccess.vue';
import FormHeader from './formComponents/FormHeader.vue';

export default {
   components: { 
     FormButtons,
     FormInputs,
     FormSuccess,
     FormHeader,
   },
   name: 'FormMain',
   data() {
      return {
         activeStep: 0,
         formSteps: [
         {
            title: "Шаг 1: Имя и почта",
            fields: [
               { 
               label: "Введите имя", 
               err: '*не менее 2-х символов', 
               value: '', 
               valid: true, 
               pattern: /.+/ 
               },
               { 
               label: "Введите вашу почту", 
               err: '*введите корректный email', 
               value: '', 
               valid: true, 
               pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/ 
               },
            ]
         },
         {
            title: "Шаг 2: Номер телефона",
            fields: [
               { 
               label: "Введите ваш номер телефона", 
               err: '*введите корректный номер телефона',
               value: '', 
               valid: true, 
               pattern: /[(][0-9]{3}[)] [0-9]{3}-[0-9]{4}/, 
               },
            ]
         },
         {
            title: "Шаг 3: Подтверждение",
         },
         ],
         formInfo: {
         name: '',
         email: '',
         phoneNumber: '',
         },
      }
   },
   methods: {
      nextStep() {
         this.activeStep += 1;
      },
      prevStep() {
         this.activeStep -=1;
      },
      validateFields() {
         let valid = true;
         this.formSteps[this.activeStep].fields.forEach(field => {
         if(!field.pattern.test(field.value) || field.value.length < 2) {
            valid = false;
            field.valid = false;
         } else {
            if(field.label === "Введите имя") {
               this.formInfo.name = field.value;
            } else if(field.label === "Введите вашу почту") {
               this.formInfo.email = field.value;
            } else {
               this.formInfo.phoneNumber = '+7 ' + field.value;
            }
            field.valid = true;
         }
         });
         if(valid) {
            this.nextStep();
         }
      },
      resetForm() {
         this.formSteps[this.activeStep].fields.forEach(field => {
            field.value = '';
         });
         this.formInfo.name = '';
         this.formInfo.email = '';
         this.formInfo.phoneNumber = '';
         this.activeStep = 0;
      },
   },
}
</script>