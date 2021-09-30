<template>
  <v-card
      elevation = "1"
      dense
      class="mail-content"
  >
    <v-card-title v-if="emailTitle"> {{ emailTitle }}</v-card-title>
    <v-card-title v-else> Email n°{{step}} </v-card-title>
    <v-card-subtitle>{{ emailDescription }}</v-card-subtitle>
    <v-card-text>
      <v-card>
        <v-card-text>
          {{ mainBodyText }}
        </v-card-text>
      </v-card>
    </v-card-text>
    <v-card-actions>
      <v-row justify="center">
        <v-btn
            class="ma-2"
            large
            color="success"
            @click="legitClick"
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
            @click="suspectClick"
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

<script>
export default {
  name: "Email",
  props: ['step'],

  data: () => ({
    mainBodyText: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.\n",
    emailDescription: "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris.",
    emailTitle: "",
    isLegit: true,

  }),
  methods: {
    legitClick() {
      this.$emit('clicked', this.isLegit === true)
    },
    suspectClick() {
      this.$emit('clicked', this.isLegit === false)
    },
  }
}
</script>

<style scoped>

</style>