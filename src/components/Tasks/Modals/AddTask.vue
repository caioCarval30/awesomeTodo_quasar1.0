<template>
  <q-card>
    <q-card-section class="row">
      <div class="text-h6">Add Task</div>
      <q-space />
      <q-btn
        v-close-popup
        flat
        dense
        round
        icon="close" />
    </q-card-section>

    <form @submit.prevent="submitForm">
      <q-card-section>
        <div class="row q-mb-sm">
          <q-input
            outlined
            v-model="taskToSubmit.name"
            label="Task Name"
            class="col"
            ref="name"
            :rules="[val => !!val || 'Field is required']" />
        </div>

        <div class="row q-mb-sm">
          <q-input
            outlined
            label="Due Date"
            v-model="taskToSubmit.dueDate">
            <template v-slot:append>
              <q-icon name="event" class="cursor-pointer">
                <q-popup-proxy ref="qDateProxy" transition-show="scale" transition-hide="scale">
                  <q-date v-model="taskToSubmit.dueDate" />
                </q-popup-proxy>
              </q-icon>
            </template>
          </q-input>
        </div>

        <div class="row q-mb-sm">
          <q-input
            outlined
            label="Due Time"
            v-model="taskToSubmit.dueTime">
            <template v-slot:append>
              <q-icon name="access_time" class="cursor-pointer">
                <q-popup-proxy transition-show="scale" transition-hide="scale">
                  <q-time v-model="taskToSubmit.dueTime"/>
                </q-popup-proxy>
              </q-icon>
            </template>
          </q-input>
        </div>
      </q-card-section>

      <q-card-actions align="right">
          <q-btn
            label="Save"
            type="submit"
            color="primary" />
      </q-card-actions>
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
      console.log('Submit Form')
      this.$refs.name.validate()
      if (!this.$refs.name.hasError) {
        this.submitTask()
      }
    },
    submitTask () {
      this.addTask()
    }
  }
}
</script>

<style>

</style>
