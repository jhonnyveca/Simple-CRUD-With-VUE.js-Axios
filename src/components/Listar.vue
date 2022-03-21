<template>
  <div class="container">
      <router-link to="/crear" class="btn btn-success">Agregar Nuevo Usuario</router-link>
      <br /><br />
    <div class="card">
      <div class="card-header">Usuarios</div>
      <div class="card-body">
        <table class="table">
          <thead>
            <tr>
              <th>ID</th>
              <th>Nombre</th>
              <th>Apellido</th>
              <th>Email</th>
              <th>Acciones</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="user in users" :key="user.id">
              <td>{{ user.id }}</td>
              <td>{{ user.user_name }}</td>
              <td>{{ user.user_lastname }}</td>
              <td>{{ user.user_email }}</td>
              <td>
                  <div class="btn-group" role="group" aria-label="">
                      <router-link :to="{name:'Editar', params:{id:user.id}}" class="btn btn-warning">Editar</router-link>
                      <button type="button" v-on:click="deleteUser(user.id)" class="btn btn-danger">Borrar</button>
                  </div>

              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      users: [],
    };
  },
  name: "ListarUser",
  created: function () {
    this.getUsers();
  },
  methods: {
    getUsers() {
      axios
        .get("http://localhost:5005/api/v1/users")
        .then((respuesta) => respuesta.data)
        .then((data) => {
          console.log(data);
          this.users = [];
          if (typeof data[0].success == "undefined") {
            this.users = data;
          }
        })
        .catch(console.error);
    },
    deleteUser(id) {
          axios
        .delete(`http://localhost:5005/api/v1/users/${id}`)
        .then((respuesta) => respuesta.data)
        .then((data) => {
          console.log(data);
         window.location.href="listar";
        })
        .catch(console.error);
    }
  },
};
</script>
