<template>
  <q-layout view="hHh Lpr fFf">
    <q-header elevated>
      <q-toolbar>

        <q-toolbar-title class="absolute-center">
          Awesome Todo
        </q-toolbar-title>

      </q-toolbar>
    </q-header>

    <q-footer>
      <q-tabs>
        <q-route-tab
          v-for="nav in navs"
          :key="nav.label"
          :to="nav.to"
          :icon="nav.icon"
          :label="nav.label"
          class="text-grey-4" />
        </q-tabs>
    </q-footer>

    <q-drawer
      v-model="leftDrawerOpen"
      :width="250"
      :breakpoint="784"
      show-if-above
      content-class="bg-primary"
      bordered>

      <q-list dark>
          <q-item-label header>Navigation</q-item-label>

      <q-item
        v-for="nav in navs"
        :key="nav.label"
        :to="nav.to"
        exact
        class="text-grey-4"
        clickable>
        <q-item-section avatar>
          <q-icon
            :name="nav.icon" />
        </q-item-section>
        <q-item-section>
          <q-item-label> {{ nav.label }}</q-item-label>
        </q-item-section>
      </q-item>

      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'

export default {
  data () {
    return {
      leftDrawerOpen: false,
      navs: [
        {
          label: 'Todo',
          icon: 'list',
          to: '/'
        },
        {
          label: 'Settings',
          icon: 'settings',
          to: '/settings'
        }
      ]
    }
  },
  methods: {
    openURL
  }
}
</script>

<style>
  @media screen and (min-width: 768px) {
    .q-footer {
      display: none;
    }
  }

  .q-drawer .q-router-link--exact-active, .q-footer .q-router-link--exact-active {
    color: white !important;
    font-weight: 600;
    text-shadow: 2px 2px rgba(0,0,0,.4);
  }
</style>
