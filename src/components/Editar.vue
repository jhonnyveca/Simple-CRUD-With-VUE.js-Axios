<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Actualizar usuario</div>
      <div class="card-body">
        <form v-on:submit.prevent="editarRegistro">
          <div class="form-group">
            <label for="" class="form-label"></label>
            <input
              type="text"
              required
              name="nombre"
              v-model="usuario.user_name"
              id="nombre"
              class="form-control"
              placeholder=""
              aria-describedby="helpId"
            />
            <small id="helpId" class="text-muted"
              >Escribe el nombre del usuario</small
            >
          </div>

          <div class="form-group">
            <label for="" class="form-label"></label>
            <input
              type="text"
              required
              name="apellido"
              id="apellido"
              v-model="usuario.user_lastname"
              class="form-control"
              placeholder=""
              aria-describedby="helpId"
            />
            <small id="helpId" class="text-muted"
              >Escribe el apellido del usuario</small
            >
          </div>

          <div class="form-group">
            <label for="" class="form-label"></label>
            <input
              type="email"
              required
              name="correo"
              id="correo"
              v-model="usuario.user_email"
              class="form-control"
              placeholder=""
              aria-describedby="helpId"
            />
            <small id="helpId" class="text-muted"
              >Escribe el correo del usuario</small
            >
          </div>
          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-warning">Editar</button>

            <router-link :to="{ name: 'Listar' }" class="btn btn-secondary"
              >Cancelar</router-link
            >
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
    name: 'EditarUser',
    data(){
   return {
      usuario: {},
    };
    },
    created:function(){
    this.getInfoById()
    },
    methods:{
        getInfoById(){
      axios
        .get("http://localhost:5005/api/v1/users/"+this.$route.params.id)
        .then((respuesta) => respuesta.data)
        .then((data) => {
          console.log(data);
         this.usuario = data[0];
         
        })
        .catch(console.error);
        },
        editarRegistro(){
        axios
        .put(`http://localhost:5005/api/v1/users/${this.$route.params.id}`, {
            id: this.$route.params.id,
          user_name: this.usuario.user_name,
          user_lastname: this.usuario.user_lastname,
          user_email: this.usuario.user_email,
        })
        .then((respuesta) => respuesta.data)
        .then((datosRespuesta) => {
          console.log(datosRespuesta);
          window.location.href = "../listar";
        });
        }
       
    },
}
</script>