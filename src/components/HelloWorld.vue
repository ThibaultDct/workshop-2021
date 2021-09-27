<template>
  <v-container>
    <v-row justify="center" align="center">
      <template v-if="step === 1">
        <v-card
        elevation = "1"
        dense
        class="mail-content"
        >
          <v-card-title>Mail {{step}}</v-card-title>
          <v-card-subtitle>Description mail 1</v-card-subtitle>
          <v-card-text>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
          </v-card-text>
          <v-card-actions>
            <v-row justify="center">
              <v-btn
              class="ma-2"
              large
              color="success"
              >
              <v-icon dark>
                mdi-check-circle-outline
              </v-icon>
              Mail légitime
              </v-btn>
              <v-btn
                class="ma-2"
                large
                color="error"
              >
                <v-icon dark>
                  mdi-close-circle-outline
                </v-icon>
                Mail suspect
              </v-btn>
            </v-row>
          </v-card-actions>
        </v-card>
      </template>
      <template v-if="step === 2">

      </template>
      <template v-if="step === 3"><!-- Step 3 Content --></template>
    </v-row>
    <template>
      <v-row justify="center">
        <v-card color="accent" dense width="50%" class="ma-2">
          <v-card-title>
            Score : {{score}}
          </v-card-title>
        </v-card>
      </v-row>
    </template>
    <v-row class="stepper">
      <v-stepper :steps="steps" v-model="step"></v-stepper>
    </v-row>
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
      score: 5,
    }),
  }
</script>

<style scoped>
  .mail-content {
    max-width: 50%;
  }

  .stepper {
    position: absolute;
    bottom: 10%;
  }
</style>
