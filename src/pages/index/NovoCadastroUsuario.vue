<template>
  <q-page class="wrapper">
    <div class="form-container">
      <TextoDinamico as="h1" style="margin: 1.8rem 0">
        Cadastrar novo usuário
      </TextoDinamico>

      <q-form class="column q-gutter-md" @submit="cadastrarUsuario">
        <CampoTexto
          placeholder="Nome completo"
          v-model="nome"
          :rules="vNome"
          outlined
        />

        <CampoTexto
          placeholder="E-mail"
          v-model="email"
          :rules="vEmail"
          outlined
        />

        <CampoTexto
          placeholder="Telefone"
          mask="(##)#.####-####"
          fill-mask
          v-model="telefone"
          :rules="vTelefone"
          outlined
        />

        <ButtonDefault label="Cadastrar" color="green" type="submit" />
      </q-form>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
import { useQuasar } from "quasar";
const $q = useQuasar();

const nome = ref("");
const email = ref("");
const telefone = ref("");

const url_api = "https://6a8529b09c451dc67a6351f4.mockapi.io/contatos";

import axios from "axios";
import CampoTexto from "@/components/CampoTexto.vue";
import ButtonDefault from "@/components/ButtonDefault.vue";
import "@/css/NovoCadastroUsuario.scss";
import TextoDinamico from "@/components/TextoDinamico.vue";

const vNome = [
  (val) => !!val || "Campo obrigatório",
  (val) => (val && val.length >= 5) || "Campo deve ter mais de 5 letras",
];

const vEmail = [
  (val) => !!val || "Campo obrigatório",
  (val) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(val) || "E-mail inválido",
];

const vTelefone = [
  (val) => !!val || "Campo obrigatório",
  (val) => !val.includes("_") || "Preencha o telefone formato (88)9.9999-1010",
  (val) => (val && val.length === 15) || "Preencha adequadamente",
];

const cadastrarUsuario = async () => {
  await axios.post(url_api, {
    nome: nome.value,
    email: email.value,
    telefone: telefone.value,
  });

  $q.notify({
    message: "Cadastrado com sucesso!",
    color: "green",
    position: "top",
    timeout: 500,
  });

  nome.value = "";
  email.value = "";
  telefone.value = "";
};
</script>
