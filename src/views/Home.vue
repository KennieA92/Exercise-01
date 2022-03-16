<template>
  <div class="home">
    <!-- <Toast v-if="showToast" /> -->
    <Todos @badValue="triggerToast" />
  </div>
</template>

<script>
// Make sure to import Toast.
import { ref } from "vue";
import Todos from "../components/Todos";

export default {
  // Make sure we can use Toast in the template.
  components: { Todos },
  setup() {
    const showToast = ref(false);

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => (showToast.value = false), 3000);
    };

    return { showToast, triggerToast };
  },
};
</script>

<style>
</style>