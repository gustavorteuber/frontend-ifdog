<script>
import { mapState } from "pinia";
import { useAuthStore } from "@/stores/auth";
import axios from "axios";

export default {
  name: "cachorros",
  props: ["id", "cachorro"],
  cachorro: {
    cachorro: 0,
    tel_responsavel: "",
  },
  methods: {
    async getAllCachorros(id) {
      await this.get(`/cachorros/${id}/`, this.cachorros);
      console.log(this.cachorros);
    },
  },
  async created() {
    const res = await axios.get(
      `https://horseti.pythonanywhere.com/cachorros/${this.id}/`
    );
    this.cachorro = res.data;
  },
  computed: {
    ...mapState(useAuthStore, ["cachorros"]),
  },
};
</script>

<template>
  <div class="card">
    <img :src="cachorro.foto.url" />
    <h1>{{ cachorro.nome }}</h1>
    <div class="descricao">
      <p>{{ cachorro.descricao }}</p>
    </div>

    <div class="button">
      <RouterLink :to="`/cachorro/${cachorro.id}`"
        ><button>clique aqui</button></RouterLink
      >
      <div class="button">
        <a target="_blank" :href="cachorro.tel_responsavel"
          >Estou em apuros? Clique aqui</a
        >
      </div>
    </div>
  </div>
</template>

<style scoped>
.descricao {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 306px;
}
</style>
