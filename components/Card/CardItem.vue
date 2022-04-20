<template>
  <div
    :class="[
      'item-task d-flex align-items-start border-bottom pt-3 pb-4',
      isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12',
    ]"
    v-if="display"
  >
    <input
      type="checkbox"
      name="status"
      id="task"
      class="me-2 mt-2"
      :checked="task.isDone"
      v-model="task.isDone"
    />
    <div
      :class="[
        'd-flex flex-column',
        task.isDone ? 'text-decoration-line-through fst-italic' : '',
      ]"
    >
      <nuxt-link class="title-task mb-1" :to="'app/detail/' + task.id">
        {{ task.title }}
      </nuxt-link>
      <div class="description-task small text-muted">
        {{ task.description }}
      </div>
      <input class="form-control form-control-sm" type="date" />
    </div>
  </div>
</template>
<script>
export default {
  props: {
    task: {
      type: Object,
      default: {
        title: "Untitled",
        description: "undescribe",
        isDone: false,
      },
    },
    isGrid: {
      type: Boolean,
      required: true,
      default: false,
    },
    hide: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  computed: {
    display() {
      if (this.hide) {
        if (this.task.isDone) {
          return false;
        } else {
          return true;
        }
      } else {
        return true;
      }
    },
  },
};
</script>
