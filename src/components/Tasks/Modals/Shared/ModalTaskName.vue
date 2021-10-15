<template>
  <div class="row q-mb-sm">
    <q-input
      autofocus
      outlined
      :value="name"
      label="Task Name"
      class="col"
      ref="name"
      :rules="[val => !!val || 'Field is required']">
      <template v-slot:append>
        <q-icon
          name="close"
          v-if="propName"
          @click="propName =''"
          class="cursor-pointer" />
      </template>
    </q-input>
  </div>
</template>

<script>
export default {
  props: ['name'],
  data () {
    return {
      propName: this.name
    }
  }
}
</script>

<style>

</style>
