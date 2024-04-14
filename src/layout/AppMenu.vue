<script setup>
import { ref } from "vue";

import AppMenuItem from "./AppMenuItem.vue";

const model = ref([
  {
    label: "Dashboard",
    items: [
      { label: "Boshqaruv paneli", icon: "pi pi-fw pi-home", to: "/" },
      { label: "Xodimlar paneli", icon: "pi pi-fw pi-user", to: "/s" },
      { label: "Bemorlar paneli", icon: "pi pi-fw pi-users", to: "/d" },
      { label: "To'lovlar paneli", icon: "pi pi-fw pi-wallet", to: "/d" },
    ],
  },
  {
    label: "Asosiy",
    items: [
      {
        label: "Taqvim",
        icon: "pi pi-fw pi-calendar",
        to: "/uikit/formlayout",
      },
      { label: "Bemorlar", icon: "pi pi-fw pi-user-minus", to: "/uikit/input" },
      {
        label: "Xodimlar",
        icon: "pi pi-fw pi-user-plus",
        to: "/uikit/floatlabel",
      },
      {
        label: "Davolashlar",
        icon: "pi pi-fw pi-plus-circle",
        to: "/uikit/invalidstate",
      },
      {
        label: "To'lovlar",
        icon: "pi pi-fw pi-dollar",
        to: "/uikit/button",
        class: "rotated-icon",
      },
      {
        label: "Xarajatlar",
        icon: "pi pi-fw pi-window-maximize",
        to: "/uikit/table",
      },
    ],
  },
  {
    label: "Hisoblar",
    items: [
      {
        label: "Hisob turlari",
        icon: "pi pi-fw pi-id-card",
        to: "/uikit/invalidstate",
      },
      {
        label: "Hisoblar",
        icon: "pi pi-fw pi-building",
        to: "/uikit/invalidstate",
      },
    ],
  },
]);
</script>

<template>
  <ul class="layout-menu">
    <template v-for="(item, i) in model" :key="item">
      <app-menu-item
        v-if="!item.separator"
        :item="item"
        :index="i"
      ></app-menu-item>
      <li v-if="item.separator" class="menu-separator"></li>
    </template>
  </ul>
</template>

<style lang="scss" scoped></style>
