<template>
  <app-drop @drop="moveTaskOrColumn">
    <app-drag
      :transfer-data="{
        type: 'task',
        fromColumnIndex: columnIndex,
        fromTaskIndex: taskIndex
      }"
    >
      <div class="task"
        @click="goToTask(task)"
      >
        <span class="w-full flex-no-shrink font-bold">
          {{ task.name }}
        </span>
        <p
        v-if="task.description"
        class="w-full flex-no-shrink text-sm mt-1"
      >
      {{ task.description }}
      </p>
      </div>
    </app-drag>
  </app-drop>
</template>

<script>
import movingTasksAndColumnsMixin from '../mixins/movingTasksAndColumnsMixin'
import AppDrag from './AppDrag'
import AppDrop from './AppDrop'

export default {
  name: 'ColumnTask',
  components: {
    AppDrop,
    AppDrag
  },
  mixins: [movingTasksAndColumnsMixin],
  props: {
    task: {
      type: Object,
      required: true
    },
    taskIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    goToTask (task) {
      this.$router.push({ name: 'task', params: { id: task.id } })
    }
  }
}
</script>

<style scoped>
  .task {
    @apply flex items-center flex-wrap shadow mb-2 py-2 px-2 rounded bg-white text-grey-darkest no-underline;
  }
</style>
