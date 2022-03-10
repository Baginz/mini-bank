<template>
  <form @submit.prevent="onSubmit">
    <div
      class="form-control"
      :class="{invalid: fError}"
    >
      <label for="fio">ФИО</label>
      <input
        id="fio"
        v-model="fio"
        type="text"
        @blur="fBlur"
      >
      <small v-if="fError">{{ fError }}</small>
    </div>

    <div
      class="form-control"
      :class="{invalid: pError}"
    >
      <label for="phone">Телефон</label>
      <input
        id="phone"
        v-model="phone"
        type="number"
        @blur="pBlur"
      >
      <small v-if="pError">{{ pError }}</small>
    </div>

    <div
      class="form-control"
      :class="{invalid: aError}"
    >
      <label for="amount">Суммы</label>
      <input
        id="amount"
        v-model.number="amount"
        type="number"
        @blur="aBlur"
      >
      <small v-if="aError">{{ aError }}</small>
    </div>

    <div class="form-control">
      <label for="status">Статус</label>
      <select
        id="status"
        v-model="status"
      >
        <option value="done">
          Завершен
        </option>
        <option value="cancelled">
          Отменен
        </option>
        <option value="active">
          Активен
        </option>
        <option value="pending">
          Выполняется
        </option>
      </select>
    </div>

    <button
      class="btn primary"
      :disabled="isSubmitting"
    >
      Создать
    </button>
  </form>
</template>

<script>

import { useStore } from 'vuex';
import { useRequestForm } from '../../use/request-form';

export default {
  emits: ['created'],
  setup(_, { emit }) {
    const store = useStore();

    const submit = async (values) => {
      await store.dispatch('request/create', values);
      emit('created');
    };

    return {
      ...useRequestForm(submit),
    };
  },
};
</script>

<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  /* display: none; <- Crashes Chrome on hover */
  -webkit-appearance: none;
  margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
}

input[type=number] {
  -moz-appearance:textfield; /* Firefox */
}
</style>
