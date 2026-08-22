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

        <!-- Percorre a lista: se tiver children renderiza o Dropdown, senão o Link Simples -->
        <template v-for="item in linksList" :key="item.label">
          <!-- DROPDOWN PARA USUÁRIO -->
          <q-expansion-item
            v-if="item.children"
            :icon="item.icon"
            :label="item.label"
            :caption="item.caption"
          >
            <EssentialLink
              v-for="subLink in item.children"
              :key="subLink.label"
              v-bind="subLink"
              class="q-pl-md"
              style="padding-left: 2.4rem"
            />
          </q-expansion-item>

          <!-- LINK SIMPLES -->
          <EssentialLink v-else v-bind="item" />
        </template>
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
  // ITEM COM DROPDOWN PARA USUÁRIO:
  {
    label: "Usuário",
    caption: "Gerenciamento",
    icon: "person",
    children: [
      {
        label: "Cadastrar",
        caption: "Novo usuário",
        icon: "person_add",
        link: "/NovoCadastroUsuario",
      },
      {
        label: "Gerenciar",
        caption: "Lista de usuários",
        icon: "manage_accounts",
        link: "/GerenciarUsuario",
      },
    ],
  },
  {
    label: "E-mail",
    caption: "Enviar mensagem",
    icon: "email",
    link: "/FormContatoUsuario",
  },
  {
    label: "Carteira",
    caption: "Digital",
    icon: "account_balance_wallet",
    link: "/CarteiraDigital",
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>

<style>
.q-drawer .q-item__section--avatar,
.q-drawer .q-item__section--side {
  min-width: 28px !important;
  padding-right: 0px !important;
  margin-right: 8px !important;
}
</style>
