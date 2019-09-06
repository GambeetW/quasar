<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar>
        <!-- <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
        >
          <q-icon name="menu" />
        </q-btn> -->

        <q-toolbar-title class="absolute-center">
          Todo list App
        </q-toolbar-title>

        <!-- <div>Quasar v{{ $q.version }}</div> -->
      </q-toolbar>
    </q-header>

    <q-footer elevated>

        <q-tabs
          v-model="tab"
          class="text-white shadow-2">
          <q-route-tab
            v-for="(nav, index) in navs"
            :key="index"
            :to="nav.to"
            :icon="nav.icon"
            :label="nav.label"
            exact />

          <!-- <q-route-tab
            to="/setting"
            icon="settings"
            label="Settings"
            exact /> -->
        </q-tabs>

    </q-footer>

    <q-drawer
      v-model="leftDrawerOpen"
      :width="250"
      :breakpoint="768"
      bordered
      content-class="bg-primary"
    >
      <q-list dark>
        <q-item-label header>Essential Links</q-item-label>
        <!-- <q-item
        to="/"
        exact
        clickable>
          <q-item-section avatar>
            <q-icon name="list" />
          </q-item-section>
          <q-item-section>
            <q-item-label>list</q-item-label>
            <q-item-label caption>Todo list</q-item-label>
          </q-item-section>
        </q-item> -->

        <q-item
        v-for="(nav, index) in navs"
        :key="index"
        :to="nav.to"
        exact
        clickable>
          <q-item-section avatar>
            <q-icon :name="nav.icon" />
          </q-item-section>
          <q-item-section>
            <q-item-label>{{ nav.label }}</q-item-label>
            <q-item-label caption>{{ nav.sub_label }}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container class="bg-indigo-1">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'

export default {
  name: 'Layout',
  data () {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop,
      navs: [
        {
          label: 'Todo list',
          sub_label: 'Todo list',
          icon: 'list',
          to: '/'
        },
        {
          label: 'Settings',
          sub_label: 'Customization',
          icon: 'settings',
          to: '/setting'
        }
      ]
    }
  },
  methods: {
    openURL
  }
}
</script>

<style lang="scss">
  /* Here the footer will be invisible until it reaches the width of the 768px XD */
  @media screen and (min-width: 768px) {
    .q-footer {
      display: none;
    }
  }
  .q-drawer {
    .q-router-link--exact-active {
      color: #ffffff !important;
      background: rgba(218, 223, 225, 0.3);
    }
  }
</style>
