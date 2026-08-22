<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> Q-App </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" bordered>
      <q-list>
        <q-item-label header> Navegação </q-item-label>

        <EssentialLink
          v-for="link in linksList"
          :key="link.label"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";
import EssentialLink from "@/components/EssentialLink.vue";

const linksList = [
  {
    label: "Home",
    caption: "Página inical",
    icon: "home",
    link: "/",
  },
  {
    label: "Carteira",
    caption: "Digital",
    icon: "account_balance_wallet",
    link: "/CarteiraDigital",
  },
  {
    label: "E-mail",
    caption: "Enviar mensagem",
    icon: "email",
    link: "/FormContatoUsuario",
  },
  {
    label: "Github",
    caption: "Repositório",
    icon: "school",
    link: "https://github.com/carlospontocom/quasar-default",
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>
