<script>
import axios from "axios";
import { mapStores, mapState } from "pinia";
import { useAuthStore } from "@/stores/auth";
export default {
  name: "tags",
  props: ["id"],
  data() {
    return {
      tags:{
        cachorro: 0,
        local:"",
    },
  };
},

  async created() {
    const res = await axios.get(`http://localhost:8000/tags/${this.id}/`);
    this.tags = res.data;
    },
    methods: {
      async alterarLoc() {
        const info = {
          local: this.tags.local,
          nome: this.cachorro.nome
        }
        try {
          await axios.put(
            `http://localhost:8000/tags/${this.id}/`,
            info)
          alert("Alterado com sucesso!")
          this.$router.push("/cachorrada");
         } catch {
          alert("Algo deu errado, tente novamente ");
        }
      },
    },
    computed: {
      ...mapStores(useAuthStore),
      ...mapState(useAuthStore, ["cachorros","username", "email", "id", "first_name"]),
    },
    mounted() {
      
    },
  };
</script>
<template>
    <div class="all">
        <div class="container">

            <div class="title">
                <h1>
                    Atualize a localização !
                </h1>
            </div>
            <div class="dogs">
            <select name="cachorros" id="localização">
                <option value="Maicon">{{tags.cachorro.nome}}</option>
                <option value="Formiga">{{tags.cachorro.nome}}</option>
                <option value="Fumaça">{{tags.cachorro.nome}}</option>
                <option value="Churras">{{tags.cachorro.nome}}</option>
            </select>
        </div>
        <div class="blocos">
            <select name="blocos" id="blocos">
                <option value="A">{{tags.local}}</option>
                <option value="B">{{tags.local}}</option>
                <option value="C">{{tags.local}}</option>
                <option value="D">{{tags.local}}</option>
                <option value="E">{{tags.local}}</option>
            </select>
        </div>
        <div class="upload">
            <button>Atualizar</button>
        </div>
    </div>
    </div>
</template>


<style scoped>

h1{
    background: -webkit-linear-gradient(45deg, #8a93e4, #00b7ff, #3071e7);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

select{
    height: 40px;
  margin-top: 1rem;
  background-color: #161e35;
  border-radius: 6px;
  color: #fff;
  outline: none;
  padding: 3% 5%;
  margin-left: 5%;
    width: 300px;
}

.upload button{
    
    margin-top:1rem ;
    width: 300px;
    height: 40px;
    border-radius: 15px;
  background: linear-gradient(to right, #0419d6, #00b7ff);
  color: #fff;
  font-weight: 500;
  cursor: pointer;

}

.upload button:hover{
    
    background: linear-gradient(to right, rgb(230, 108, 169), #970584);}

.container{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

    .all{
        margin-top: 15rem ;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
</style>