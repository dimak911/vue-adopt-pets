<template>
  <div>
    <h1>{{ species | capitalize }} for adoption</h1>
    <b-table striped hover :items="pets">
      <template #cell(name)="data">
        <router-link :to="`/pets/${species}/${data.index}`">{{
          data.value
        }}</router-link>
      </template>
    </b-table>
  </div>
</template>

<script>
export default {
  props: {
    species: String,
    pets: Array,
  },
  filters: {
    capitalize: function (value) {
      if (!value) return "";
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    },
  },
};
</script>
