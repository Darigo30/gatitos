<template>
  <div id="app">
    <div class="container mt-5">
      <div class="row">
        <div class="col-12 bg-celeste">
          <h1>Random Gif Cat</h1>
        </div>
        <!-- Formulario de consulta -->
        <div class="col-12 bg-rosado">
          <div class="my-3">
            <div class="form-group row">
              <label class="col-sm-2 col-form-label">Título</label>
              <div class="col-sm-10">
                <input type="text" class="form-control my-2" v-model="nombre_gato">
              </div>
            </div>
            <div class="form-group row">
              <label class="col-sm-2 col-form-label">Filtro</label>
              <div class="col-sm-10">
                <select class="form-select my-2" v-model="filtro_color">
                  <option>sepia</option>
                  <option>mono</option>
                  <option>blur</option>
                  <option>negative</option>
                  <option>paint</option>
                  <option>pixel</option>
                </select>
              </div>
            </div>
             <div class="form-group row">
              <label class="col-sm-2 col-form-label">Color</label>
              <div class="col-sm-8">
                <select class="form-select my-2" v-model="colores">
                  <option v-for="(el, index) in modelocolor" :value="el.valor" :key="index">
                    {{el.nombrecolor}}
                    </option>
                </select>
              </div>
              <div class="col-sm-2">
                <div class="circulo" :class="colorcir"></div>
              </div>
            </div>
            
            <div class="form-group row">
              <label class="col-sm-2 col-form-label">Tamaño</label>
              <div class="col-sm-10">
                <input type="text" @keypress="validar()" class="form-control my-2" v-model="tamano_gato">
               <div class="noesun" id="noesun"></div> 
              </div>
            </div>
          </div>
          <button type="button" class="btn btn-primary mt-1 fw-bold" @click="getGato">Obtener mi Gatito</button>
        </div>
      </div>
      <!-- Fin Formulario de consulta -->
      <!-- Resultados de gatitos aqui -->
      <div v-show="mostrar" class="row mt-4">
        <img :src="imagen" />
      </div>
      <!-- Fin Resultados de gatitos aqui -->
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      nombre_gato: "",
      filtro_color: "",
      tamano_gato: "",
      imagen: "",
      colores: "",
      mostrar: false,
      modelocolor: [
        {
          nombrecolor: "verde",
          valor: "green",
        },
        {
          nombrecolor: "azul",
          valor: "blue",
        },
        {
          nombrecolor: "rojo",
          valor: "red",
        },
        {
          nombrecolor: "amarillo",
          valor: "yellow",
        },
        {
          nombrecolor: "blanco",
          valor: "white",
        },
      ],
    };
  },
  methods: {
    async getGato() {
      this.mostrar = false;
      const url = `https://cataas.com/cat/gif/says/${this.nombre_gato}?filter=${this.filtro_color}&color=${this.colores}&size=${this.tamano_gato}`;
      try {
        const req = await axios(url);
        if (!req) return;
        this.imagen = url;    
        console.log(this.imagen);
        this.mostrar = true;
        if(this.nombre_gato == "" || this.filtro_color == "" || this.colores == "" || this.tamano_gato == "") return
         this.nombre_gato = ""
         this.filtro_color = ""
         this.colores = ""
         this.tamano_gato = ""
      } catch (error) {
        console.log(error);
      }
    },
    validar() {
      if(isNaN(`${this.tamano_gato}`)){
        const noesun = document.getElementById("noesun");
        noesun.innerHTML += "Debe ingresar un número"
      }
    },
  },
  computed: {
    colorcir(){
      return{
        "verde": (this.colores === "green"),
        "rojo": (this.colores === "red"),
        "blanco": (this.colores === "white"),
        "amarillo": (this.colores === "yellow"),
        "azul": (this.colores === "blue"),
      }
    }
  },
};

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
}
.container{
  width: 450px;
}
h1{
    font-weight: bold;
}
.circulo{
  width: 80%;
  height: 80%;
  border: 1px solid rgb(255, 255, 255);
  border-radius: 50%;
}
.verde{
  background-color: green;
}
.rojo{
  background-color: red;
}
.azul{
  background-color: blue;
}
.blanco{
  background-color: white;
}
.amarillo{
  background-color: yellow;
}
.bg-celeste{
  background-color: rgb(36, 208, 214);
  padding: 10px 0;
  color: #fff;
}
.bg-rosado{
  background-color: rgb(190, 61, 162);
  padding: 15px;
}
label{
  color: #fff;
}
.noesun{
  color: white;
  font-weight: bold;
  text-align: left;
}

</style>
