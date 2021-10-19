<template>
  <q-page padding>

    <noTasks
      v-if="!Object.keys(tasksTodo).length" />

    <tasksTodo
      v-else
      :tasksTodo="tasksTodo" />

    <tasksCompleted
      v-if="Object.keys(tasksCompleted).length"
      :tasksCompleted="tasksCompleted" />

    <div class="absolute-bottom text-center q-mb-xl">
      <q-btn
        @click="showAddTask = true"
        :ripple="false"
        round
        color="primary"
        size="20px"
        icon="add"
      />
    </div>

    <q-dialog v-model="showAddTask">
      <addTask @close="showAddTask = false" />
    </q-dialog>

  </q-page>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  data () {
    return {
      showAddTask: false
    }
  },
  computed: {
    ...mapGetters('tasks', ['tasksTodo', 'tasksCompleted'])
  },
  components: {
    addTask: require('components/Tasks/Modals/AddTask.vue').default,
    tasksTodo: require('components/Tasks/TasksTodo.vue').default,
    tasksCompleted: require('components/Tasks/TasksCompleted.vue').default,
    noTasks: require('components/Tasks/NoTasks.vue').default
  },
  mounted () {
    this.$root.$on('showAddTask', () => {
      this.showAddTask = true
    })
  }
}
</script>
