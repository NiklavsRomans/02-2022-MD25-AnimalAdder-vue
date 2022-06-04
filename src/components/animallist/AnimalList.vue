<template>
  <li
    class="animal-list"
    :key="id"
    v-for="({ id, name, type }, index) in animals"
  >
    <div class="animal-type">{{ type }}</div>
    {{ name }}
    <div>
      <button @click="handleDelete(index)" class="delete-btn">X</button>
    </div>
  </li>
</template>

<script lang="ts">
import { defineComponent } from "@vue/runtime-core";

export default defineComponent({
  name: "AnimalList",
  emits: ["deleteAnimal"],
  props: {
    animals: { type: [Array, Object], required: true },
  },
  data() {
    return {};
  },

  methods: {
    handleDelete(index: number) {
      this.$emit("deleteAnimal", index);
    },
  },
});
</script>

<style scoped lang="scss">
@import "AnimalList.scss";
</style>
