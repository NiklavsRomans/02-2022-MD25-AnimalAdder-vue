<template>
  <div class="form-container">
    <form @submit.prevent="handleSubmit">
      <input
        required
        class="input"
        placeholder="Add new animal..."
        v-model="inputValue"
        type="text"
      />
      <select required v-model="animalType" class="select">
        <option value="" disabled>Type</option>
        <option value="cat">Cat</option>
        <option value="dog">Dog</option>
      </select>
      <button class="add-btn" type="submit">Add</button>
    </form>
  </div>
</template>

<script>
import { defineComponent } from "@vue/runtime-core";

export default defineComponent({
  name: "AnimalForm",
  emits: ["addAnimal"],
  data() {
    return {
      inputValue: "",
      animalType: "",
    };
  },

  methods: {
    handleSubmit() {
      this.$emit("addAnimal", {
        id: Math.random() * 1000,
        type: this.animalType,
        name: this.inputValue,
      });
      this.inputValue = "";
    },
  },
});
</script>

<style scoped lang="scss">
@import "AnimalForm.scss";
</style>
