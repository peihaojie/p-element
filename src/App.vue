<!--
 * @Author: HaoJie
 * @Date: 2023-01-29 14:27:39
 * @LastEditTime: 2023-01-29 14:30:28
 * @LastEditors: HaoJie
 * @FilePath: \p-element\src\App.vue
-->
<template>
  <div id="app">
    <div style="display: flex; justify-content: center">
      <p-select v-model="aaa" :optionList="list" />
    </div>
  </div>
</template>

<script>
import pSelect from "@/components/pSelect.vue";

export default {
  name: "App",
  components: {
    pSelect,
  },
  data() {
    return {
      aaa: 1,
      list: [
        {
          label: "咳咳咳1",
          value: 1,
        },
        {
          label: "咳咳咳2",
          value: 2,
        },
        {
          label: "咳咳咳3",
          value: 3,
        },
        {
          label: "咳咳咳4",
          value: 4,
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
