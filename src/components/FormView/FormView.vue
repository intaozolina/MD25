<template>
  <div class="form_box">
    <form class="form" @submit.prevent="submitHandler">
      <input
        class="form__input"
        ref="inputRef"
        type="text"
        required
        placeholder="Add new animal ..."
        v-model="inputValue"
      />
      <select class="form__select" v-model="selectValue">
        <option value="" disabled>Type</option>
        <option value="cat">Cat</option>
        <option value="dog">Dog</option>
      </select>
      <button class="form__submit-btn" type="submit">ADD</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "./formView.scss";

export default defineComponent({
  name: "FormView",
  emits: ["addAnimal"],
  data: () => ({
    inputValue: "",
    selectValue: "",
  }),
  methods: {
    submitHandler() {
      this.$emit("addAnimal", this.inputValue, this.selectValue);
      this.inputValue = "";
    },
  },
});
</script>
