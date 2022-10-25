<template>
  <v-text-field
    @click:append="addTask"
    @keyup.enter="addTask"
    class="pa-3"
    outlined
    label="Add Task"
    clearable
    hide-details
    v-model="newTaskTitle"
  >
    <template v-slot:append>
      <v-fade-transition leave-absolute>
        <v-progress-circular
          v-if="loading"
          size="24"
          color="info"
          indeterminate
        ></v-progress-circular>
        <img
          v-else
          width="24"
          height="24"
          src="https://cdn.vuetifyjs.com/images/logos/v-alt.svg"
          alt=""
        />
      </v-fade-transition>
    </template>
  </v-text-field>
</template>

<script>
export default {
  data() {
    return {
      newTaskTitle: "",
    };
  },
  methods: {
    addTask() {
      this.$store.dispatch("addTask", this.newTaskTitle);
      this.newTaskTitle = "";
    },
  },
};
</script>
