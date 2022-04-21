<template>
  <ul>
    <li :class="{ darkMode: darkMode, active: modelValue === 'poor' }">
      <button type="button" @click="selectedOption('poor')">Poor</button>
    </li>
    <li :class="{ darkMode: darkMode, active: modelValue === 'avg' }">
      <button type="button" @click="selectedOption('avg')">Average</button>
    </li>
    <li :class="{ darkMode: darkMode, active: modelValue === 'great' }">
      <button type="button" @click="selectedOption('great')">Great</button>
    </li>
  </ul>
</template>
<script>
export default {
  //For custom components
  props: ['modelValue', 'darkMode'],
  emits: ['update:modelValue'],
  // data() {
  //   return {
  //     selectedBtn: this.modelValue,
  //   };
  // },
  //   computed: {
  //     selectedBtn() {
  //       return this.modelValue;
  //     },
  //   },
  methods: {
    selectedOption(name) {
      //   this.selectedBtn = name;
      this.$emit('update:modelValue', name);
    },
  },
};
</script>
<style scoped>
.active {
  border-color: aqua;
}
/* .active button {
  color: aqua;
} */
ul {
  list-style: none; /* Remove HTML bullets */
  margin: 0.5rem 0;
  padding: 0;
  display: flex;
  overflow: auto;
}
li {
  display: flex;
  align-content: center;
  justify-content: center;
  padding: 1rem;
  border: 1px solid #ccc;
  margin: 0 1rem;
}
button {
  font: inherit;
  border: none;
  background-color: transparent;
  cursor: pointer;
  color: black;
}
.darkMode button {
  color: white;
}
</style>
