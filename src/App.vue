<template>
  <div id="app">
    <div class="container mt-5">
      <div class="row">
        <div class="col-12">
          <h1>Random Gif Cat</h1>
        </div>
        <!-- Formulario de consulta -->
        <div class="col-12">
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
                 <select id="disabledSelect" class="form-select my-2" v-model="filtro_color">
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
                <select id="disabledSelect" class="form-select my-2">
                  <option>Rojo</option>
                </select>
              </div>
              <div class="col-sm-2">
                <div class="circulo"></div>
              </div>
            </div>
            
            <div class="form-group row">
              <label class="col-sm-2 col-form-label">Tamaño</label>
              <div class="col-sm-10">
                <input type="number" class="form-control my-2" v-model="tamano_gato">
              </div>
            </div>
          </div>
          <button type="button" class="btn btn-primary mt-1" @click="getGato">Obtener mi Gatito</button>
        </div>
      </div>
      <!-- Fin Formulario de consulta -->
      <!-- Resultados de gatitos aqui -->
      <div class="row">
         <img :src="imagen">
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
    };
  },
  methods: {
    async getGato() {
      const url = `https://cataas.com/cat/gif/says/${this.nombre_gato}?filter=${this.filtro_color}&color=orange&size=${this.tamano_gato}`;
      try {
        const req = await axios(url);
        if (!req) return;
        this.imagen = req.data;
    
        if(this.nombre_gato == "" || this.filtro_color == "" ||  this.tamano_gato == "") return
         this.nombre_gato = ""
         this.filtro_color = ""
         this.tamano_gato = ""
      } catch (error) {
        console.log(error);
      }
    },
  },
  created () {
    this.getGato();
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
  border: 1px solid rebeccapurple;
  background: red;
  border-radius: 50%;
}
</style>
