
<template>
  <div>
    <div>
      <TodoItens />

    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import TodoItens from '@/components/TodoItens';
export default {
  name: 'App',
  components: { TodoItens },
  setup() {
    const loading = ref(false);
    loading.value = true
    return {
      loading,
    }
  },
}

</script>

<style>
.contentt {
  justify-content: center;
  align-content: center;
  align-items: center;
  background-color: aquamarine;
}
</style>