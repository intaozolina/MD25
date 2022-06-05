<template>
  <div class="form-check form-switch form-check-reverse">
    <input
      class="form-check-input"
      type="checkbox"
      id="flexSwitchCheckReverse"
      @change="switchHandler"
    />
    <label class="form-check-label" for="flexSwitchCheckReverse">Cats</label>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "SwitcherView",
  emits: ["switchToCats"],
  data: () => ({
    switched: false,
  }),
  methods: {
    switchHandler() {
      this.switched = !this.switched;
      this.$emit("switchToCats", this.switched);
    },
  },
});
</script>
