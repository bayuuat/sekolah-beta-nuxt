<template>
  <div class="container">
    <h2>task id:{{ this.$route.params.id }}</h2>
    <div v-for="task in tasks" :key="task.id">
      <div
        class="item-task d-flex align-items-start pt-3 pb-4"
        v-if="task.id == paramId"
      >
        <input
          type="checkbox"
          name="status"
          id="task"
          class="me-2 mt-2"
          :checked="task.isDone"
          v-model="task.isDone"
        />
        <div>
          <div class="title-task mb-1">
            {{ task.title }}
          </div>
          <div class="description-task small text-muted mb-3">
            {{ task.description }}
          </div>
          <input class="form-control form-control-sm" type="date" />
        </div>
      </div>
    </div>
    <div class="action mt-4">
      <div
        class="btn btn-outline-secondary btn-sm mb-3"
        @click="$router.go(-1)"
      >
        Kembali
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      paramId: this.$route.params.id,
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
};
</script>
