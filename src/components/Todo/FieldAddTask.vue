<template>
  <v-text-field
    @keyup.enter="addTask"
    class="pa-3"
    outlined
    label="Add Task"
    clearable
    hide-details
    v-model="newTaskTitle"
  >
    <template v-slot:append>
      <v-icon @click="addTask" color="primary" :disabled="!newTaskTitle"
        >mdi-plus</v-icon
      >
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
  computed: {
    newTaskTitleInvalid() {
      return !this.newTaskTitle;
    },
  },
  methods: {
    addTask() {
      if (!this.newTaskTitleInvalid) {
        this.$store.dispatch("addTask", this.newTaskTitle);
        this.newTaskTitle = "";
      }
    },
  },
};
</script>
