<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom">
        <h5 class="red">Task</h5>
      </div>
      <div class="list-task">
        <div class="item-task d-flex align-items-start border-bottom pt-3 pb-4">
          <input
            type="checkbox"
            name="status"
            id="task"
            class="me-2 mt-2"
            :checked="tasks[0].isDone"
          />
          <div class="d-flex flex-column">
            <div class="title-task mb-1">
              {{ tasks[0].title }}
            </div>
            <div class="description-task small text-muted">
              {{ tasks[0].description }}
            </div>
          </div>
        </div>
      </div>
      <div class="action py-2">
        <!-- Jika isCreating == false maka tombol Add Task tidak akan tampil -->
        <!-- isCreating = !isCreating berfungsi sebagai switcher toggle -->
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

      <!-- ========================================================================= -->
      <div class="">
        <p>Menggunakan v-html directive: <span v-html="rawHtml"></span></p>
        <button v-bind:disabled="isButtonDisabled">Button</button>
        <div class="">
          {{ number + 1 }}
          {{ ok ? "YES" : "NO" }}
          {{ message.split("").reverse().join("") }}
        </div>
        <div v-bind:id="'list-' + id"></div>
        <p v-if="seen">I'm true</p>
        <p v-if="!seen">I'm false</p>
        <a v-bind:href="url"> href langsung </a>
        <div>
          <a v-bind:[attributeName]="url"> href add atribute </a>
        </div>
        <a
          v-on:click="doSomething"
          v-bind:class="{ active: isActive, danger: hasError }"
        >
          ini tombol
        </a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      rawHtml:
        '<div class="action py-2"><a href="#" class="add-button">Add Task</a></div>',
      isButtonDisabled: true,
      number: 1,
      ok: 1,
      message: "LOOP",
      id: 1,
      seen: 1,
      url: "https://github.com/",
      attributeName: "href",
      isCreating: false,
      isActive: true,
      hasError: true,
      tasks: [
        {
          title: "Task #1 Pertama",
          description: "ini deskripsi dari task pertama",
          isDone: true,
        },
      ],
    };
  },
  methods: {
    doSomething() {
      alert("wew :D");
    },
  },
};
</script>
<style>
.red {
  color: brown;
}
.active {
  border: 3px solid black;
  color: whitesmoke;
}
.danger {
  background-color: red;
}
</style>
