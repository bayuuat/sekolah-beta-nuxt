<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center py-2">
        <h5>Task</h5>
        <div class="d-flex align-items-center ms-auto">
          <button
            class="btn btn-outline-primary py-1 px-3 me-4"
            @click="shuffle"
          >
            Shuffle!
          </button>
          <select
            class="form-select mx-3"
            name="category"
            id="category"
            v-model="sortBy"
            @change="sort"
          >
            <option value="">Sort</option>
            <option value="asc">Ascending</option>
            <option value="desc">Descending</option>
          </select>
          <select
            class="form-select mx-3"
            name="category"
            id="category"
            v-model="dropdownQuery"
          >
            <option value="">Select category</option>
            <option
              v-for="(task, i) in uniqueCategory"
              :key="i"
              :value="task.category"
            >
              {{ task.category }}
            </option>
          </select>
          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />
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
      <transition-group name="tasks" tag="div" class="list-task row">
        <CardItem
          v-for="task in resultQuery"
          :task="task"
          :key="task.id"
          :isGrid="isGrid"
          :hide="hide"
        />
      </transition-group>
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
              <input
                class="form-control border-0 mb-2"
                placeholder="Title"
                type="text"
              />
              <textarea
                class="form-control border-0 small"
                placeholder="Description"
                rows="3"
              ></textarea>
            </div>
          </div>
          <div class="button-wrapper d-flex">
            <button class="btn btn-primary me-2">Save</button>
            <button
              class="btn btn-outline-secondary"
              @click="isCreating = !isCreating"
            >
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
#app .tasks-move {
  transition: 0.4s;
}
</style>
<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },
  data() {
    return {
      isCreating: false,
      isActive: true,
      hasError: true,
      isGrid: false,
      // Variabel penampung teks pencarian
      searchQuery: "",
      dropdownQuery: "",
      sortBy: "",
      hide: false,
      // Status saat menambahkan task
      isCreating: false,
      // Tipe layout daftar task
      isGrid: false,
      tasks: [
        {
          id: 1,
          title: "Brainstroming for new Ideas",
          description: "ini deskripsi",
          isDone: false,
          category: "Manage",
        },
        {
          id: 2,
          title: "Approve and Assign ideas",
          description: "ini deskripsi 2",
          isDone: false,
          category: "Manage",
        },
        {
          id: 3,
          title: "Work on design and UX",
          description: " ini deskripsi 3",
          isDone: false,
          category: "Design",
        },
        {
          id: 4,
          title: "Publish and deploy",
          description: "ini deskripsi 4",
          isDone: false,
          category: "Develop",
        },
        {
          id: 5,
          title: "Assign topics to writer",
          description: "ini deskripsi 5",
          isDone: false,
          category: "Manage",
        },
        {
          id: 6,
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
    shuffle() {
      this.tasks = _.shuffle(this.tasks);
    },
    sort() {
      if (this.sortBy) {
        this.tasks = _.orderBy(this.tasks, ["title"], [this.sortBy]);
      }
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
