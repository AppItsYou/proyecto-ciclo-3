<template>
  <div class="row justify-content-center">
    <div class="col-md-6">
      <h3 class="text-center">Registrar Usuario</h3>
      <div v-if="esGuardado" class="alert alert-success" role="alert">
        Usuario ingresado satisfactoriamente
      </div>
      <!--  <div v-else class="alert alert-danger" role="alert">
      Estudiante no ingresado 
      </div> -->
      <form @submit.prevent="handleSubmitForm">
        <br />
        <br />
        <div class="form-group">
          <label>Nombre Completo</label>
          <input
            type="text"
            class="form-control"
            v-model="usuario.nombre"
            required
          />
        </div>
        <br />
        <div class="form-group">
          <label>Email</label>
          <input
            type="email"
            class="form-control"
            v-model="usuario.email"
            required
          />
        </div>
        <br />
        <div class="form-group">
          <label>Ingrese Password</label>
          <input
            type="password"
            class="form-control"
            v-model="usuario.password"
            required
          />
        </div>
        <br />
        <div class="form-group">
          <label>Ingrese Password Nuevamente</label>
          <input
            type="password"
            class="form-control"
            v-model="passwordEscritoNuevamente"
            required
          />
        </div>
        <br />
        
        <br />
        <div class="form-group">
          <button class="btn btn-primary">Crear cuenta</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import ruta from '../../rutaAPI';
export default {
  data() {
    return {
      passwordEscritoNuevamente: "",
      mensaje: "",
      esGuardado: false,
      usuario: {
        nombre: "",
        email: "",
        password: "",
        imagenPerfil: "",
        tipo_usuario: "regular",
      },
      files: null,
    };
  },
  methods: {
    handleSubmitForm() {
      let apiURL = `${ruta.ruta_api}/usuario-servicios/crear-usuario`;
      if (this.usuario.password == this.passwordEscritoNuevamente) {
        axios
          .post(apiURL, this.usuario)
          .then(() => {
            this.$router.push("/registro-usuario");
            this.usuario = {
              nombre: "",
              email: "",
              password: "",
              imagenPerfil: "",
              tipo_usuario: "regular",
            };
            this.passwordEscritoNuevamente = "";
          })
          .catch((error) => {
            console.log(error);
          });
        alert("Usuario ingresado");
        this.esGuardado = true;
      } else {
        this.esGuardado = false;
        alert("Los campos de pasword no coincide");
      }
    },
    
  },
};
</script>
