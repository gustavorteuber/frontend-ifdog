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
                <option value="Maicon">Maicon</option>
                <option value="Formiga">Formiga</option>
                <option value="Fumaça">Fumaça</option>
                <option value="Churras">Churras</option>
            </select>
        </div>
        <div class="blocos">
            <select name="blocos" id="blocos">
                <option value="A">A</option>
                <option value="B">B</option>
                <option value="C">C</option>
                <option value="D">D</option>
                <option value="E">E</option>
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