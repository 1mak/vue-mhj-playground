<template>
  <div class="LearningSessions-container">
    <h1>Working with Forms</h1>

    My name is <span class="highlight">{{ firstname }} {{ lastname }}</span> and
    I am {{ age }} years old.

    <form @submit.prevent="submitForm" :class="formClass">
      <label for="firstname">Firstname</label>
      <input
        type="text"
        id="firstname"
        ref="firstnameRef"
        v-model="firstname"
      />
      <hr />

      <label for="firstname">Lastname</label>
      <input type="text" ref="lastnameRef" id="lastname" v-model="lastname" />
      <hr />

      <label for="birthday">Birthday</label>
      <input type="date" ref="birthdayRef" id="birthday" v-model="birthday" />
      <hr />
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script setup>
import { ref, computed, reactive } from "vue";
import TextInput from "../components/forms/TextInput.vue";

const firstname = ref("");
const lastname = ref("");
const birthday = ref("");

// Use reactive for nested objects
const formStatus = reactive({
  isSubmitted: false,
  hasErrors: false,
});

const firstnameRef = ref("");
const lastnameRef = ref("");
const birthdayRef = ref("");

const age = computed(() => {
  const today = new Date();
  const birthDate = new Date(birthday.value);
  return today.getFullYear() - birthDate.getFullYear();
});

const formClass = computed(() => {
  if (formStatus.hasErrors) {
    return "has-errors";
  } else if (formStatus.isSubmitted) {
    return "success";
  }
  return null;
});

function submitForm() {
  formStatus.isSubmitted = true;
  formStatus.hasErrors =
    firstname.value.length < 3 ||
    lastname.value.length < 3 ||
    birthday.value.length < 1;

  if (firstname.value.length < 3) {
    firstnameRef.value.focus();
  } else if (lastname.value.length < 3) {
    lastnameRef.value.focus();
  } else if (birthday.value.length < 1) {
    birthdayRef.value.focus();
  }
}
</script>
<style lang="scss">
.highlight {
  font-weight: bold;
}
form {
  margin: 10px 0;
  padding: 20px;
  background: #eaeaea;
  label {
    margin-right: 10px;
    font-weight: bold;
  }
  hr {
    margin: 10px 0;
  }

  &.has-errors {
    background: #f2dede;
  }
  &.success {
    background: #dff0d8;
  }
}
</style>
