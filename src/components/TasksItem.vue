<template>
  <li
    class="relative p-3 pl-12 border-gray-700 border-b cursor-pointer select-none last:border-b-0"
    :class="{ 'line-through': task.isDone }"
    data-test="task"
    @click="toggleTaskDone"
  >
    <span class="absolute top-0 left-0 p-3">
      <font-awesome-icon
        v-if="task.isDone"
        class="text-green-300"
        data-test="task-is-done"
        size="lg"
        :icon="['fas', 'check-circle']"
      />
      <font-awesome-icon
        v-else
        class="text-gray-500"
        data-test="task-is-not-done"
        size="lg"
        :icon="['far', 'check-circle']"
      />
    </span>
    {{ task.name }}
    <span
      class="absolute top-0 right-0 p-3"
      data-test="remove-task-button"
      @click.stop="removeTask"
    >
      <font-awesome-icon class="text-red-600" icon="trash" />
    </span>
  </li>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "TasksItem",
  props: {
    task: {
      type: Object,
      required: true
    }
  },
  emits: ["toggle", "remove"],
  setup(props, { emit }) {
    const toggleTaskDone = () => {
      emit("toggle", props.task.id);
    };
    const removeTask = () => {
      emit("remove", props.task.id);
    };

    return {
      toggleTaskDone,
      removeTask
    };
  }
});
</script>
