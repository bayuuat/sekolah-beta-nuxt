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
          v-for="(iniisinya, i) in resultQuery"
          :key="i"
          :task="iniisinya"
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
        title: "",
        description: "",
      },
      tasks: [
        {
          title: "Brainstroming for new Ideas",
          description: "ini deskripsi",
          isDone: false,
          category: "Manage",
        },
        {
          title: "Approve and Assign ideas",
          description: "ini deskripsi 2",
          isDone: false,
          category: "Manage",
        },
        {
          title: "Work on design and UX",
          description: " ini deskripsi 3",
          isDone: false,
          category: "Design",
        },
        {
          title: "Publish and deploy",
          description: "ini deskripsi 4",
          isDone: false,
          category: "Develop",
        },
        {
          title: "Assign topics to writer",
          description: "ini deskripsi 5",
          isDone: false,
          category: "Manage",
        },
        {
          title: "Design layout",
          description: " ini deskripsi 6",
          isDone: false,
          category: "Design",
        },
      ],
    };
  },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else if (this.dropdownQuery) {
        return this.tasks.filter((item) => {
          return this.dropdownQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.category.toLowerCase().includes(v));
        });
      } else {
        return this.tasks;
      }
    },
    uniqueCategory() {
      return this.tasks.filter(
        (value, index, self) =>
          self.map((item) => item.category).indexOf(value.category) == index
      );
    },
  },
  methods: {
    handleSubmit() {
      this.tasks.push({
        title: this.form.title,
        description: this.form.description,
        isDone: false,
        category: "Manage",
      });
      this.form.title = "";
      this.form.description = "";
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
