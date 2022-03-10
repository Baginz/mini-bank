<template>
  <form
    class="card"
    @submit.prevent="onSubmit"
  >
    <h1>
      <router-link
        v-if="$route.name !== 'Auth'"
        to="/auth"
      >
        Войти в систему
      </router-link>
      <span v-else>Войти в систему</span>
      /
      <router-link
        v-if="$route.name !== 'SignUp'"
        to="/signup"
      >
        Зарегистрироваться
      </router-link>
      <span v-else>Зарегистрироваться</span>
    </h1>

    <div :class="['form-control', {invalid: eError}]">
      <label for="email">Email</label>
      <input
        id="email"
        v-model="email"
        type="email"
        @blur="eBlur"
      >
      <small v-if="eError">{{ eError }}</small>
    </div>

    <div :class="['form-control', {invalid: pError}]">
      <label for="password">Пароль</label>
      <input
        id="password"
        v-model="password"
        type="password"
        @blur="pBlur"
      >
      <small v-if="pError">{{ pError }}</small>
    </div>

    <button
      class="btn primary"
      type="submit"
      :disabled="isSubmitting || isTooManyAttempts"
    >
      Войти
    </button>
    <div
      v-if="isTooManyAttempts"
      class="text-danger"
    >
      Вы слишком часто пытаетесь. Попробуйте позже
    </div>
  </form>
</template>

<script>
import { useRoute } from 'vue-router';
import { useStore } from 'vuex';
import { error } from '../utils/error';
import { useSignUpForm } from '../use/signup-form';

export default {
  setup() {
    const route = useRoute();
    const store = useStore();

    if (route.query.message) {
      store.dispatch('setMessage', {
        value: error(route.query.message),
        type: 'warning',
      });
    }
    return { ...useSignUpForm() };
  },
};
</script>

<style scoped>

</style>
