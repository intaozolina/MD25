<template>
  <div class="hero">
    <SwitcherView @switchToCats="switchFilter" />
    <FormView @addAnimal="addAnimal" />
    <AnimalList :animals="animalsToShow" @removeById="removeFromList" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AnimalList from "@/components/AnimalList/AnimalList.vue";
import FormView from "@/components/FormView/FormView.vue";
import SwitcherView from "@/components/Switcher/Switcher.vue";
import "./homeView.scss";

export type Animal = {
  id: number;
  name: string;
  species: string;
};

export default defineComponent({
  name: "HomeView",
  data: () => ({
    animals: [] as Animal[],
    onlyCatsVisible: false,
  }),
  components: {
    SwitcherView,
    FormView,
    AnimalList,
  },
  created() {
    this.animals = JSON.parse(localStorage.getItem("animals") || "[]");
  },
  computed: {
    animalsToShow() {
      if (this.onlyCatsVisible) {
        return this.animals.filter(({ species }) => species === "cat");
      }

      return this.animals;
    },
  },
  methods: {
    addAnimal(animalName: string, animalSpecie: string) {
      const newAnimals = [
        ...this.animals,
        {
          id: this.animals.length + 1,
          name: animalName,
          species: animalSpecie,
        },
      ];
      this.animals = newAnimals;
    },
    removeFromList(index: number) {
      const newAnimals = [...this.animals];

      newAnimals.splice(index, 1);

      this.animals = newAnimals;
    },
    switchFilter(switcher: boolean) {
      this.onlyCatsVisible = !switcher;
    },
  },
  watch: {
    animals(newAnimals) {
      localStorage.setItem("animals", JSON.stringify(newAnimals));
    },
  },
});
</script>
