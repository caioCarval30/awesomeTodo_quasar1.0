<template>
  <div>
    <listHeader
      bgColor="bg-orange-6">Todo</listHeader>

    <q-list
      separator
      bordered>

      <task
        v-for="(task, key) in tasksTodo"
        :key="key"
        :task="task"
        :id="key"></task>
    </q-list>

  </div>
</template>

<script>
export default {
  props: ['tasksTodo'],
  components: {
    task: require('components/Tasks/Task.vue').default,
    listHeader: require('components/Shared/ListHeader.vue').default
  }

}
</script>
