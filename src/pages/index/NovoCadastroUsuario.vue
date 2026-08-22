<template>
  <q-page class="wrapper">
    <div class="form-container">
      <h2>Novo usuário</h2>

      <q-form class="column q-gutter-md" @submit="cadastrarUsuario">
        <CampoTexto
          placeholder="Nome completo"
          v-model="nome"
          :rules="validarNome"
        />

        <CampoTexto
          placeholder="E-mail"
          v-model="email"
          :rules="validarEmail"
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
import CampoTexto from "@/components/CampoTexto.vue";
import ButtonDefault from "@/components/ButtonDefault.vue";
import "@/css/NovoCadastroUsuario.scss";

const validarNome = [
  (val) => !!val || "Campo obrigatório",
  (val) => (val && val.length >= 5) || "Campo deve ter mais de 5 letras",
];

const validarEmail = [
  (val) => !!val || "Campo obrigatório",
  (val) => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(val) || "E-mail inválido",
];

const cadastrarUsuario = () => {
  $q.notify({
    message: "Cadastrado com sucesso!",
    color: "green",
    position: "top",
    timeout: 500,
  });
};
</script>
