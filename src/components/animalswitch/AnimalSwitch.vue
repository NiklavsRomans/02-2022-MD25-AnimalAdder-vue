<template>
  <div class="form-check form-switch">
    <input
      v-on:change="handleCatToggle"
      v-model="type"
      class="form-check-input"
      type="checkbox"
      role="switch"
    />
    <label class="form-check-label">Show Cats</label>
  </div>
</template>

<script>
import { defineComponent } from "@vue/runtime-core";

export default defineComponent({
  name: "catToggle",
  emits: ["toggleCats"],
  data() {
    return {
      type: false,
    };
  },
  methods: {
    handleCatToggle() {
      this.$emit("toggleCats", this.type);
    },
  },
});
</script>

<style></style>
