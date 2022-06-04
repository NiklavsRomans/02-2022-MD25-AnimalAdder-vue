<template>
  <div class="app-container">
    <div class="cat-toggle">
      <CatToggle @toggleCats="toggleCats" />
    </div>
    <div class="app-form">
      <AnimalForm @addAnimal="addAnimal" />
      <div class="app-form-list">
        <AnimalList @deleteAnimal="deleteAnimal" :animals="animalsView" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AnimalForm from "@/components/animalform/AnimalForm.vue";
import AnimalList from "@/components/animallist/AnimalList.vue";
import CatToggle from "@/components/animalswitch/AnimalSwitch.vue";

type AnimalProps = {
  name: string;
  id: number;
  type: string;
};

type ViewMode = "all" | "only-cats";

export default defineComponent({
  name: "App",
  components: {
    AnimalForm,
    AnimalList,
    CatToggle,
  },
  data: () => {
    return {
      animals: [] as AnimalProps[],
      viewMode: "all" as ViewMode,
    };
  },

  computed: {
    animalsView() {
      if (this.viewMode === "only-cats") {
        return this.handleOnlyCats;
      }
      return this.animals;
    },

    handleOnlyCats() {
      const filteredCats = this.animals.filter(
        (animal) => animal.type === "cat"
      );
      return filteredCats;
    },
  },

  created() {
    const savedAnimals = JSON.parse(localStorage.getItem("animal") || "[]");
    this.animals = savedAnimals || [];
  },

  watch: {
    animals(newAnimals) {
      localStorage.setItem("animal", JSON.stringify(newAnimals));
    },
  },

  methods: {
    setAnimals() {
      const newAnimals = [...this.animals];
      this.animals = newAnimals;
      return newAnimals;
    },

    toggleCats(type: boolean) {
      `${type ? (this.viewMode = "only-cats") : (this.viewMode = "all")}`;
    },

    addAnimal(animal: AnimalProps) {
      this.setAnimals().push(animal);
    },

    deleteAnimal(index: number) {
      this.setAnimals().splice(index, 1);
    },
  },
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  .app-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    background-color: lightblue;
    max-width: 650px;
    margin: 100px auto;
    border-radius: 8px;
    padding: 40px;
  }

  .cat-toggle {
    display: flex;
    margin-left: 240px;
    padding-bottom: 20px;
  }
}
</style>
