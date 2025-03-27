<template>
  <div class="px-2 lg:px-0">
    <div class="w-auto max-w-md px-6 py-6 mx-auto text-neutral-content/50 rounded-2xl">
      <h2 class="mb-4 text-2xl font-semibold text-center text-neutral-content">
        Reset your password
      </h2>
      <form
        class="space-y-3"
        @submit.prevent="submit"
      >
        <FormInputText
          v-model="form.email"
          type="email"
          label="Enter your user account's verified email address and we will send you a password reset link."
          name="email"
          data-cy="email-verification-form"
        />
      <button type="submit" name="submit" data-cy="email-verification-form-submit" class="w-full btn btn-primary">
        Send password reset email
      </button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { type Ref } from "vue";
import { EmailOnSignup, type PublicSettings } from "torrust-index-types-lib";
import { notify } from "notiwind-ts";
import { ref, useRestApi, useSettings } from "#imports";

const revealPasswords: Ref<Boolean> = ref(false);

type Form = {
  email: string,
}

const rest = useRestApi();

const form: Ref<Form> = ref({
  email: ""
});

function submit () {
  sendResetPasswordLink();
}

function sendResetPasswordLink () {
  rest.value.user.sendPasswordResetLink({
    email: form.value.email,
  })
    .then(() => {
      navigateTo("/signin", { replace: true });
      notify({
        group: "success",
        title: "Success",
        text: "Your account was registered!"
      }, 4000); // 4s
    })
    .catch((err) => {
      notify({
        group: "error",
        title: "Error",
        text: `Registration failed. ${err.message}.`
      }, 10000);
    });
}
</script>

<style scoped>

</style>
