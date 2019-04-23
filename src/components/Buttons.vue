<template>
  <div>
    <button
      v-for="(item, key) in list"
      :key="key"
      :class="['btn',{'active': item.status}]"
      @click="onEvent(key)"
    >{{item.name}}</button>
  </div>
</template>

<script>
import Vue from "vue";
export default {
  name: "buttons",
  props: ["list", status],
  methods: {
    onEvent(key) {
      this.$emit("change-status", {
        key
      });
    }
  }
};
</script>
<style scope>
.btn {
  margin-left: 5px;
  margin-right: 5px;
  font-size: 1.1em;
  border-radius: 5px;
  border-color: transparent;
  box-shadow: 0 1px 2px 1px rgba(0, 0, 0, 0.15),
    0 2px 5px -3px rgba(0, 0, 0, 0.15);
  color: rgba(0, 0, 0, 0.5);;
  background: rgba(0, 0, 0, 0.25);

  cursor: pointer;
  outline: none;
}
.active {
  color: black;
  background: white;
}
</style>


