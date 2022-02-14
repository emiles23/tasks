<!-- Please remove this file from your project -->
<template>
  <div class="min-h-screen bg-gray-100 flex flex-col justify-center pt-14">
    <button
      @click="addTask()"
      class="flex justify-end px-20 border border-none"
    >
      <add class="pt-34" />
    </button>
    <div class="relative flex items-top justify-center sm:items-center sm:pt-0">
      <link
        href="https://cdn.jsdelivr.net/npm/tailwindcss@2.1.2/dist/tailwind.min.css"
        rel="stylesheet"
      />
      <ul class="w-3/5 bg-white text-center sm:rounded-lg border">
        <h1 class="py-3 text-2xl leading-7 font-semibold">Listas de Tareas</h1>
        <template v-for="(task, index) in tasks">
          <li
            :key="index"
            class="grid justify-items-center grid-cols-3 border py-4"
          >
            <input
              @click="updateTaskStatus(index)"
              v-model="task.status"
              :checked="task.status"
              type="checkbox"
            />
            <input
              v-if="updateIndexTask == index"
              class="
                appearance-none
                rounded-none
                px-3
                py-2
                w-full
                border-b border-green-600
                placeholder-gray-500
                text-gray-900
                focus:outline-none focus:ring-secondary-500 focus:ring-1
                sm:text-sm
              "
              type="text"
              v-model="task.name"
            />
            <span v-else> {{ task.name }}</span>

            <div class="grid justify-items-center grid-cols-2">
              <button
                @click="saveTask(index)"
                v-if="updateIndexTask != null && updateIndexTask == index"
              >
                Guardar
              </button>
              <button  @click="updateTask(index)" v-else><edit /></button> 
              <button><delete /></button>
            </div>
          </li>
        </template>
      </ul>
    </div>
  </div>
</template>

<script>
import Edit from "@/components/icons/Edit";
import Delete from "@/components/icons/Delete";
import Add from "@/components/icons/Add";

export default {
  components: {
    Edit,
    Delete,
    Add,
  },
  data() {
    return {
      updateIndexTask: null,
      tasks: [
        { name: "Aprender js", status: true },
        { name: "Aprender Ingles", status: false },
        { name: "Aprender vue.js", status: false },
        { name: "Aprender React", status: false },
      ],
    };
  },

  methods: {
    addTask() {
      if (
        this.updateIndexTask != null &&
        this.tasks[this.updateIndexTask].name == ""
      ) {
        return;
      }
      this.tasks = [{ name: "", status: false }, ...this.tasks]
        this.updateIndexTask = 0;
    },

    saveTask(index) {
      if (this.tasks[index].name == "") {
        return;
      }
      this.updateIndexTask = null;
    },

    updateTask(index) {
      this.updateIndexTask = index
    },

    deleteTask(index) {
      this.tasks[index].status;
    },
  },
};
</script>
