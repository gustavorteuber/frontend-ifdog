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
      const res = await axios.get(`http://localhost:8000/tags/`);
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
          alert("LOCALIZAÇÃO ATUALIZADA!")
          this.$router.push("/comentarios");
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
            <select v-model="tags.cachorro" name="cachorros" id="tags.id">
                <option value="17">Maicon</option>
                <option value="18">Formiga</option>
                <option value="19">Churras</option>
                <option value="20">Fumaça</option>
            </select>
        </div>
        <div class="blocos">
            <select v-model="tags.local" name="blocos" id="tags.id">
                <option value="5">A</option>
                <option value="4">B</option>
                <option value="3">C</option>
                <option value="2">D</option>
                <option value="1">E</option>
            </select>
        </div>
        <div class="upload">
            <button @click="editarTag()">Atualizar</button>
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