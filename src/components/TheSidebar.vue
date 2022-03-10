<template>
  <Transition name="slide-fade">
    <div
      v-if="sidebar"
      class="sidebar"
    >
      <span
        class="sidebar-close"
        @click="close"
        @keydown.esc="close"
      >&times;</span>

      <div class="sidebar-content">
        <p>
          Добро пожаловать в систему по учету заявок в нашем банке.
          Здесь вы найдете исчерпывающую информацию про систему и заявки
        </p>
      </div>
    </div>
  </Transition>
</template>

<script>
import {computed} from 'vue';
import {useStore} from 'vuex';

export default {
  setup() {
    const store = useStore();

    const sidebar = computed(() => store.state.sidebar);

    return {
      sidebar,
      close: () => store.commit('closeSidebar'),
    };
  },
};
</script>

<style scoped>
.slide-fade-enter-active {
  transition: all 0.6s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.4s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(100px);
  opacity: 0;
}
</style>
