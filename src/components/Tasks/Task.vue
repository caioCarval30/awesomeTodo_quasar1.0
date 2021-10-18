<template>
  <q-item
    @click="updateTask({ id: id, updates: { completed: !task.completed } })"
    :class="!task.completed ? 'bg-orange-2' : 'bg-green-3'"
    clickable
    v-ripple>
    <q-item-section side top>
      <q-checkbox
        :value="task.completed"
        @input="updateTask({ id: id, updates: { completed: !task.completed } })" />
    </q-item-section>

    <q-item-section>
      <q-item-label
        :class="{ 'text-strikethrough' : task.completed }">{{ task.name }}</q-item-label>
    </q-item-section>

    <q-item-section
      v-if="task.dueDate"
      side>
      <div class="row">
        <div class="column justify-center">
          <q-icon
            name="event"
            size="18px"
            color="black"
            class="q-mr-xs" />
        </div>
        <div class="column">
          <q-item-label
            class="row justify-end"
            caption>{{ task.dueDate }}</q-item-label>
          <q-item-label
            class="row justify-end"
            caption>
            <small>{{ task.dueTime }}</small>
          </q-item-label>
        </div>
      </div>
    </q-item-section>

    <q-item-section side>
      <div class="row">
        <q-btn
          @click.stop="showEditTask = true"
          flat
          round
          dense
          color="blue-8"
          icon="edit" />
        <q-btn
          @click.stop="promptToDelete(id)"
          flat
          round
          dense
          color="negative"
          icon="delete" />
      </div>
    </q-item-section>

    <q-dialog v-model="showEditTask">
      <editTask
        @close="showEditTask = false"
        :task="task"
        :id="id" />
    </q-dialog>

  </q-item>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  props: ['task', 'id'],
  data () {
    return {
      showEditTask: false
    }
  },
  methods: {
    ...mapActions('tasks', ['updateTask', 'deleteTask']),
    promptToDelete (id) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Are you sure you want to delete this task?',
        ok: true,
        cancel: {
          color: 'negative'
        },
        persistent: false
      }).onOk(() => {
        this.deleteTask(id)
      })
    }
  },
  components: {
    editTask: require('components/Tasks/Modals/EditTask.vue').default
  }
}
</script>

<style>
  div.row .justify-end {
    color: black;
  }
</style>
