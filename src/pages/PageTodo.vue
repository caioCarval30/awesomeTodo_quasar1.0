<template>
  <q-page padding>

    <tasksTodo
      :tasksTodo="tasksTodo" />

    <tasksCompleted
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
    tasksCompleted: require('components/Tasks/TasksCompleted.vue').default
  }
}
</script>
