<template>
  <v-container>
    <template v-if="step === 1">
      <v-card
      elevation = "1"
      dense
      >
        <v-card-title>Mail {{step}}</v-card-title>
        <v-card-subtitle>Personnaliser l'apparence de votre interface</v-card-subtitle>
        <v-card-text>
          
        </v-card-text>
      </v-card>
    </template>
    <template v-if="step === 2"><!-- Step 2 Content --></template>
    <template v-if="step === 3"><!-- Step 3 Content --></template>
    <v-stepper :steps="steps" v-model="step"></v-stepper>
  </v-container>
</template>

<script>
import { VStepper } from 'vue-stepper-component'

  export default {
    name: 'HelloWorld',
    
    components: {VStepper},

    data: () => ({
      steps: 10,
      step: undefined,
    }),
  }
</script>
