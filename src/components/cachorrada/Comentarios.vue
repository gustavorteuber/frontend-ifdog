<script>
import axios from "axios";
import { mapState } from "pinia";
import { useAuthStore } from "@/stores/auth";
export default {
  props: ["comentarios"],
  data() {
    return {
      superuser: "",
      value: 1,
      user: {},
    };
  },
  methods: {
    async removerComentario() {
      await axios.delete(
        `http://localhost:8000/coments/${this.comentarios.id}/`
      );
      this.$swal("Comentario deletado com sucesso!"),
        this.$router.push("/cachorrada");
    },
  },
  computed: {
    ...mapState(useAuthStore, ["is_superuser"]),
  },
};
</script>

<template>
  <div class="full">
    <div class="comentarios">
      <RouterLink to="/singout"
        ><h1>{{ comentarios.autor.username }}</h1></RouterLink
      >
      <div class="fuso">
        <h2>{{ comentarios.texto }}</h2>
        <a>{{ comentarios.data }}</a>
      </div>
      <div class="remove" v-bind="superuser">
        <button
          v-if="is_superuser == true"
          @click="
            this.id = comentarios.autor.id;
            removerComentario();
          ">
          DELETAR
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.leaflet-popup-content-wrapper,
.leaflet-popup-tip {
  background-color: #161e35;
}
.remove {
  display: flex;
  align-items: center;
}
.fuso a {
  font-size: 10pt;
  background: -webkit-linear-gradient(45deg, #8a93e4, #00b7ff, #3071e7);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
button {
  cursor: pointer;
  color: #eff;
  height: 30px;
  width: 60px;
  border-radius: 16px;
  background: red;
}
.comentarios {
  max-height: 500px;
  max-width: 750px;
  border-radius: 0px 10px 10px 10px;
  border: 1px solid #eef;
  background-color: #161e35;
  display: flex;
  margin-top: 20px;
  margin-left: 20px;
}

h1 {
  background: -webkit-linear-gradient(45deg, #8a93e4, #00b7ff, #3071e7);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-size: 16pt;
}

h2 {
  word-break: break-all;
  margin-top: 7px;
  margin-left: 10px;
  font-size: 10pt;
}

.full {
  max-width: 500px;
  margin-left: 5%;
  display: flex;
  color: #eff;
}
</style>
