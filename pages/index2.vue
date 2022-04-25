<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center py-2">
        <h5>Task</h5>
        <div class="d-flex align-items-center ms-auto">
          <span>Hide</span>
          <div class="tg-list-item ms-3">
            <input
              type="checkbox"
              name=""
              id="cb1"
              class="tgl tgl-light"
              v-model="hide"
            />
            <label class="tgl-btn" for="cb1"></label>
          </div>
          <div class="d-flex align-items-center justify-content-end w-100">
            <span class="me-2">View As</span>
            <button
              class="btn btn-outline-secondary py-1 px-3"
              @click="isGrid = !isGrid"
            >
              {{ isGrid ? "Grid" : "List" }}
            </button>
          </div>
        </div>
      </div>
      <div class="list-task row">
        <CardItem
          v-for="(task, i) in tasks"
          :key="i"
          :task="task"
          :isGrid="isGrid"
          :hide="hide"
        />
      </div>
      <div class="action py-2">
        <a
          href="#"
          class="add-button"
          v-if="!isCreating"
          @click="isCreating = !isCreating"
          >Add Task</a
        >
        <div class="add-card" v-else>
          <div class="card mb-2">
            <div class="card-body d-flex flex-column p-0">
              <form v-on:submit.prevent="handleSubmit">
                <input
                  class="form-control border-0 mb-2"
                  placeholder="Title"
                  type="text"
                  v-model="form.title"
                />
                <textarea
                  class="form-control border-0 small"
                  placeholder="Description"
                  rows="3"
                  v-model="form.description"
                ></textarea>
                <div class="button-wrapper d-flex">
                  <button class="btn btn-primary me-2">Save</button>
                  <button
                    class="btn btn-outline-secondary"
                    @click="isCreating = !isCreating"
                  >
                    Cancel
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },
  data() {
    return {
      isLoading: true,
      isCreating: false,
      isActive: true,
      hasError: true,
      isGrid: false,
      // Variabel penampung teks pencarian
      searchQuery: "",
      dropdownQuery: "",
      hide: false,
      // Status saat menambahkan task
      isCreating: false,
      // Tipe layout daftar task
      isGrid: false,
      form: {
        id: 3,
        title: "",
        description: "",
        isDone: false,
      },
    };
  },
  computed: {
    tasks() {
      return this.$store.state.tasks.tasks;
    },
  },
  methods: {
    handleSubmit() {
      this.form.id += 1;

      var payload = this.form;

      this.$store.dispatch("tasks/addTask", payload);

      this.form = {
        title: "",
        description: "",
        isDone: false,
      };
    },
  },
};
</script>
<style>
.red {
  color: brown;
}
.active {
  border-bottom: 3px solid black;
  color: whitesmoke;
}
.danger {
  background-color: red;
}
</style>
