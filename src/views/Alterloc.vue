<script>
  import { mapState, mapStores } from "pinia";
  import { useAuthStore } from "@/stores/auth";
  import axios from "axios";
  export default {
    data() {
      return {
        tags: {
          id: "",
          local:{
            id:"",
            local:"",
            hardware:"",
          }
        },
      };
    },
      async created() {
      const res = await axios.get(`http://localhost:8000/tags/${this.id}/`);
      this.tags = res.data;
      console.log(this.tags)
  },
    methods: {
      async editarTag() {
        const info = {
          local: this.tags.local,
          cachorro: this.tags.cachorro,
        }
        try {
          await axios.put(
            `http://localhost:8000/tags/${this.id}/`,
            info)
          alert("por favor deslogar para salvar as informações")
         } catch {
          alert("Algo deu errado, tente novamente ");
        }
      },
    },
    computed: {
      ...mapStores(useAuthStore),
      ...mapState(useAuthStore, ["username", "email", "id", "first_name"]),
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
            <select v-model="tags.cachorro" name="cachorros" id="localização">
                <option value="Maicon">{{tags.cachorro}}</option>
                <option value="Formiga">{{tags.cachorro}}</option>
                <option value="Fumaça">{{tags.cachorro}}</option>
                <option value="Churras">{{tags.cachorro}}</option>
            </select>
        </div>
        <div class="blocos">
            <select v-model="tags.local" name="blocos" id="blocos">
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