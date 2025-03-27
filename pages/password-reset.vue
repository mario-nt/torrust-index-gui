<template>
  <EmailVerificationForm />
</template>

<script setup lang="ts">
import EmailVerificationForm from "~/components/password-reset/EmailVerificationForm.vue";
// v-if="emailVerified == false"

let resetEmailSent = false;

function ToggleState () {
  if (emailVerified === false) {
    emailVerified = true;
  } else {
    emailVerified = false;
  }
}


</script>

  <style scoped>

  </style>
