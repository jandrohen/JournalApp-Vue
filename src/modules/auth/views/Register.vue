<script>
import { defineComponent, ref } from "vue";
import useAuth from "@/modules/auth/composables/useAuth";
import { useRouter } from "vue-router";

import Swal from "sweetalert2";
export default defineComponent({
  name: "Register",
  setup() {
    const router = useRouter();
    const { createUser } = useAuth();
    const userForm = ref({
      name: "",
      email: "",
      password: "",
    });

    return {
      userForm,

      onSubmit: async () => {
        const { ok, message } = await createUser(userForm.value);
        ok
          ? router.push({ name: "no-entry" })
          : Swal.fire("Error", message, "error");
      },
    };
  },
});
</script>

<template>
  <span class="login100-form-title p-b-41"> Create Account </span>
  <form
    class="login100-form validate-form p-b-33 p-t-5"
    @submit.prevent="onSubmit"
  >
    <div class="wrap-input100 validate-input" data-validate="Enter username">
      <input
        v-model="userForm.name"
        class="input100"
        type="text"
        placeholder="Name"
        required
      />
      <span class="focus-input100" data-placeholder="&#xe82a;"></span>
    </div>

    <div class="wrap-input100 validate-input" data-validate="Enter email">
      <input
        v-model="userForm.email"
        class="input100"
        type="email"
        placeholder="Email"
        autocomplete="username"
        required
      />
      <span class="focus-input100" data-placeholder="&#xe818;"></span>
    </div>

    <div class="wrap-input100 validate-input" data-validate="Enter password">
      <input
        v-model="userForm.password"
        class="input100"
        type="password"
        placeholder="Password"
        autocomplete="current-password"
        required
      />
      <span class="focus-input100" data-placeholder="&#xe80f;"></span>
    </div>

    <div class="container-login100-form-btn m-t-32">
      <button type="submit" class="login100-form-btn">Create Account</button>
    </div>

    <div class="container-login100-form-btn m-t-32">
      <router-link :to="{ name: 'login' }"
        >Do you already have an account?</router-link
      >
    </div>
  </form>
</template>

<style scoped lang="scss"></style>
