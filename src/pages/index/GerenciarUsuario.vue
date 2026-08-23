<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import TextoDinamico from "@/components/TextoDinamico.vue";
import CampoTexto from "@/components/CampoTexto.vue";
import ButtonDefault from "@/components/ButtonDefault.vue";

const usuarios = ref([]);
const exibirForm = ref(false);

const url_api = "https://6a8529b09c451dc67a6351f4.mockapi.io/contatos";

const buscarUsuarios = async () => {
  const response = await axios.get(url_api);
  usuarios.value = response.data;
};

onMounted(() => {
  buscarUsuarios();
});

const removerUsuario = async (id) => {
  await axios.delete(`${url_api}/${id}`);
  usuarios.value = usuarios.value.filter((item) => item.id !== id);
};

const atualizarDadosUsuario = async (id) => {
  exibirForm.value = true;
};

const salvarEdicao = async () => {
  exibirForm.value = false;
};
</script>

<template>
  <q-page class="container">
    <TextoDinamico as="h1">Gerenciar usuários</TextoDinamico>
    <ul>
      <li>Pesquisar</li>
      <li>Editar</li>
      <li>Excluir</li>
    </ul>

    <!-- Adicionado @submit para capturar o envio e fechar o formulário -->
    <q-form v-if="exibirForm" class="column q-gutter-md" @submit="salvarEdicao">
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

      <ButtonDefault label="Salvar dados" color="green" type="submit" />
    </q-form>

    <ul>
      <li v-for="usuario in usuarios" :key="usuario.id" class="card">
        <div>
          <p>{{ usuario.nome }}</p>
          <p>{{ usuario.email }}</p>
          <p>{{ usuario.telefone }}</p>
          <q-btn label="x" color="red" @click="removerUsuario(usuario.id)" />
          <q-btn
            label="Editar"
            color="orange"
            @click="atualizarDadosUsuario(usuario.id)"
          />
        </div>
      </li>
    </ul>
  </q-page>
</template>

<style scoped>
.container {
  padding: 25px;
}
ul {
  padding: 0;
  margin: 1.8rem 0 0 0;
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 1rem;

  @media (min-width: 568px) {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }

  @media (min-width: 900px) {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    max-width: 1024px;
    margin: 0 auto;
  }
}

.card {
  padding: 1rem;
  border: 1px solid #ccc;
}
</style>