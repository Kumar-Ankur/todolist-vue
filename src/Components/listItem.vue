<template>
  <div class="row">
    <ul class="list-group list-group-flush">
      <app-item v-for="(task, index) in tasks" :key="task" :index="index" :task="task">{{ task }}</app-item>
    </ul>
  </div>
</template>
<script>
import Item from "./Item.vue";
export default {
  props: ["tasks"],
  components: {
    appItem: Item
  }
};
</script>

<style scoped>
</style>