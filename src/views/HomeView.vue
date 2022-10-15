<template>
  <div class="home-view-container">
    <h1>Adopt a new best friend.</h1>
    <p>Total pets: {{ animalsCount }}</p>
    <button class="btn btn-primary mb-2" @click="togglePetForm">
      Add New Pet
    </button>
    <b-form @submit.prevent="handleSubmit" v-if="showPetForm" class="addForm">
      <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="formData.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Species:" label-for="input-2">
        <b-form-select
          id="input-2"
          v-model="formData.species"
          :options="['cats', 'dogs']"
          class="w-100"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-3" label="Pet's Age:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="formData.age"
          placeholder="Enter age"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary" class="mt-2">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
  name: "HomeView",
  data() {
    return {
      showPetForm: false,
      formData: {
        name: "",
        age: 0,
        species: null,
      },
    };
  },
  computed: {
    ...mapGetters(["animalsCount"]),
  },
  methods: {
    ...mapActions(["addPet"]),
    togglePetForm() {
      this.showPetForm = !this.showPetForm;
    },
    handleSubmit() {
      const { species, name, age } = this.formData;
      const payload = {
        species,
        pet: {
          name,
          age,
        },
      };
      this.addPet(payload);

      //reset form
      this.formData = {
        name: "",
        age: 0,
        species: null,
      };
    },
  },
};
</script>

<style scoped>
.addForm {
  margin: 0 auto;
  max-width: 400px;
}
</style>
