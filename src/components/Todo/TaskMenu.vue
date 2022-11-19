<template>
  <div>
    <v-menu bottom left>
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="primary" icon v-bind="attrs" v-on="on">
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          @click="handleClick(i)"
        >
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <dailog-edit
      v-if="dialogs.edit"
      @close="dialogs.edit = false"
      :task="task"
    ></dailog-edit>
    <dailog-due-date
      v-if="dialogs.dueDate"
      @close="dialogs.dueDate = false"
      :task="task"
    ></dailog-due-date>
    <dailog-delete
      v-if="dialogs.delete"
      @close="dialogs.delete = false"
      :task="task"
    ></dailog-delete>
  </div>
</template>

<script>
import DialogDelete from "./Dialogs/DialogDelete.vue";
import DialogEdit from "./Dialogs/DialogEdit.vue";
import DialogDueDate from "./Dialogs/DialogDueDate.vue";
export default {
  props: ["task"],
  components: {
    "dailog-delete": DialogDelete,
    "dailog-edit": DialogEdit,
    "dailog-due-date": DialogDueDate,
  },
  data: () => ({
    dialogs: {
      delete: false,
      edit: false,
      dueDate: false,
    },
    items: [
      {
        title: "Edit",
        icon: "mdi-pencil",
        click() {
          this.dialogs.edit = true;
        },
      },
      {
        title: "Due date",
        icon: "mdi-calendar",
        click() {
          this.dialogs.dueDate = true;
        },
      },
      {
        title: "Delete",
        icon: "mdi-delete",
        click() {
          this.dialogs.delete = true;
        },
      },
    ],
  }),
  methods: {
    handleClick(index) {
      this.items[index].click.call(this);
    },
  },
};
</script>

<style>
</style>