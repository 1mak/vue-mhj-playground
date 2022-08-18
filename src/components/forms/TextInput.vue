<template>
  <div class="text-input-container">
    <label :for="props.label">{{ props.label }}</label>
    <input
      type="text"
      :id="props.label"
      :ref="`${props.label}Ref`"
      :value="modelValue"
      @input.prevent="changeInput"
    />
    <hr />
  </div>
</template>

<script setup>
const props = defineProps({
  label: {
    type: String,
    value: "Firstname",
  },
  modelValue: {
    type: String,
    value: "",
  },
});
const emit = defineEmits(["update:modelValue"]);

function changeInput(event) {
  emit("update:modelValue", event.target.value);
}
</script>

<style lang="scss">
label {
  margin-right: 10px;
  font-weight: bold;
  text-transform: capitalize;
}
</style>
