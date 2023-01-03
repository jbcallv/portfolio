<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="q-pa-md" style="background: #121212">
      <q-toolbar>
        <q-btn
          class="lt-md"
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> JOSEPH CALL </q-toolbar-title>

        <q-tabs v-model="tab" class="gt-md" indicator-color="accent">
          <q-route-tab
            v-for="link in essentialLinks"
            :key="link.title"
            :name="link.name"
            :label="link.title"
            :to="link.link"
          />
        </q-tabs>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" class="lt-md bg-dark">
      <q-list>
        <q-item-label header> Joseph Call </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container class="q-px-md">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    title: "Home",
    icon: "school",
    link: "/",
    name: "docs",
  },
  {
    title: "Projects",
    icon: "school",
    link: "/projects",
    name: "projects",
  },
  {
    title: "About",
    icon: "school",
    link: "/about",
    name: "about",
  },
  {
    title: "Contact",
    icon: "phone",
    link: "/contact",
    name: "contact",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },

  setup() {
    const leftDrawerOpen = ref(false);
    const tab = ref("docs");

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
      tab,
    };
  },
});
</script>
