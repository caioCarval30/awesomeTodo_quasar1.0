<template>
  <q-page padding>
    <q-list
      v-if="Object.keys(tasks).length"
      separator
      bordered>

      <task
        v-for="(task, key) in tasks"
        :key="key"
        :task="task"
        :id="key"></task>

    </q-list>

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
      <addTask @closeAddTask="showAddTask = false" />
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
    ...mapGetters('tasks', ['tasks'])
  },
  components: {
    task: require('components/Tasks/Task.vue').default,
    addTask: require('components/Tasks/Modals/AddTask.vue').default
  }
}
</script>
