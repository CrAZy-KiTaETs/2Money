<script>
import { computed, ref } from "vue";
import { useStore } from "vuex";
import catalogOpen from "@/assets/images/catalog-open.png";
import catalogClose from "@/assets/images/catalog-close.png";

export default {
  name: "HeaderPage",
  setup(props, { emit }) {
    const store = useStore();
    const mainSum = computed(() => store.getters.mainSum);

    const activeWindow = ref("main");

    const changeWindow = (window) => {
      activeWindow.value = window;

      emit("changeWindow", window);
    };
    return {
      mainSum,
      activeWindow,
      changeWindow,
      catalogOpen,
      catalogClose
    };
  },
};
</script>

<template>
  <header class="header">
    <div class="general_money">
      <p class="general_money-text">Мой счет</p>
      <p class="general_money-count">{{ mainSum }}</p>
    </div>

    <button
      class="history-btn"
      v-if="activeWindow === 'main'"
      @click="changeWindow('history')"
    >
      <img :src="catalogClose" alt="" />
    </button>
    <button
      class="history-btn"
      v-else-if="activeWindow === 'history'"
      @click="changeWindow('main')"
    >
      <img :src="catalogOpen" alt="" />
    </button>
  </header>
</template>

<style lang="scss">
@import "./Header.scss";
</style>