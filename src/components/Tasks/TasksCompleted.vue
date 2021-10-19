<template>
  <div class="q-mt-lg">
    <listHeader
      bgColor="bg-green-8">Completed</listHeader>

    <q-list
      separator
      bordered>

      <task
        v-for="(task, key) in tasksCompleted"
        :key="key"
        :task="task"
        :id="key"></task>
    </q-list>

  </div>
</template>

<script>
export default {
  props: ['tasksCompleted'],
  components: {
    task: require('components/Tasks/Task.vue').default,
    listHeader: require('components/Shared/ListHeader.vue').default
  }

}
</script>
