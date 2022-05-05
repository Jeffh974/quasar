<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevate class="flex">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title class="flex flex-center">
          Quasar App
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      behavior="mobile"
      :mini="mini"
      @mouseover="mini = false"
      @mouseout="mini = true"
      mini-to-overlay
      :width="200"
      :breakpoint="500"
      bordered
      overlay
    >

      <q-item-label header>
        Essential Links
      </q-item-label>

      <q-scroll-area class="fit">
        <q-list padding>
          <q-item clickable>
            <q-item-section avatar>
              <q-icon name="inbox"/>
            </q-item-section>

            <q-item-section>
              Inbox
            </q-item-section>
          </q-item>

        </q-list>
      </q-scroll-area>


      <q-list>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>

    </q-drawer>

    <q-page-container>
      <router-view/>
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import {defineComponent, ref} from 'vue';
import EssentialLink from 'components/EssentialLink.vue';
import {linksList} from 'components/Const';

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  setup() {
    const leftDrawerOpen = ref(false)

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      mini: ref(true)
    }
  }
});
</script>
