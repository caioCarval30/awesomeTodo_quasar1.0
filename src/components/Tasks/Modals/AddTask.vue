<template>
  <q-card>

    <modalHeader>Add Task</modalHeader>

    <form @submit.prevent="submitForm">
      <q-card-section>

        <modalTaskName
          :name.sync="taskToSubmit.name"
          ref="modalTaskName" />

        <modalDueDate
          :dueDate.sync="taskToSubmit.dueDate"
          @clear="clearDueDate" />

        <modalDueTime
          v-if="taskToSubmit.dueDate"
          :dueTime.sync="taskToSubmit.dueTime"/>

      </q-card-section>

      <modalButtons />

    </form>

  </q-card>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  data () {
    return {
      taskToSubmit: {
        name: '',
        dueDate: '',
        dueTime: '',
        completed: false
      }
    }
  },
  methods: {
    ...mapActions('tasks', ['addTask']),
    submitForm () {
      this.$refs.modalTaskName.$refs.name.validate()
      if (!this.$refs.modalTaskName.$refs.name.hasError) {
        this.submitTask()
      }
    },
    submitTask () {
      this.addTask(this.taskToSubmit)
      this.$emit('close')
    },
    clearDueDate () {
      this.taskToSubmit.dueDate = ''
      this.taskToSubmit.dueTime = ''
    }
  },
  components: {
    modalHeader: require('components/Tasks/Modals/Shared/ModalHeader.vue').default,
    modalTaskName: require('components/Tasks/Modals/Shared/ModalTaskName.vue').default,
    modalDueDate: require('components/Tasks/Modals/Shared/ModalDueDate.vue').default,
    modalDueTime: require('components/Tasks/Modals/Shared/ModalDueTime.vue').default,
    modalButtons: require('components/Tasks/Modals/Shared/ModalButtons.vue').default
  }
}
</script>
