<template>
  <div class="animal__hero">
    <ul class="animal__list">
      <li
        class="animal__list-item"
        :key="singleAnimal.id"
        v-for="singleAnimal in this.animals"
      >
        <div class="animal__list-species">
          {{ singleAnimal.species.toUpperCase() }}
        </div>
        <span class="animal__list-name">{{
          singleAnimal.name.toUpperCase()
        }}</span>
        <button
          class="animal__list-btn"
          @click="removeHandler(singleAnimal.id)"
        >
          X
        </button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { Animal } from "@/views/HomeView.vue";
import "./animalList.scss";

export default defineComponent({
  name: "AnimalList",
  props: ["animals"],
  emits: ["removeById"],
  methods: {
    removeHandler(id: number) {
      const index = this.animals.findIndex(
        (animal: Animal) => animal.id === id
      );
      this.$emit("removeById", index);
    },
  },
});
</script>
