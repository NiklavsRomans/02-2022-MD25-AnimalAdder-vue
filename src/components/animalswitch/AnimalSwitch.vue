<template>
  <div class="form-check form-switch">
    <input
      @change="handleCatToggle"
      class="form-check-input"
      type="checkbox"
      role="switch"
      v-model="selected"
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
      selected: false,
    };
  },
  methods: {
    handleCatToggle() {
      this.$emit("toggleCats", this.selected);
    },
  },
});
</script>

<style></style>
