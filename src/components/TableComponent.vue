<template>
  <div>
    <h2 class="text-center">Tabla de usuarios</h2>
    <table class="table table-striped}">
      <tr>
        <th>Nombre</th>
        <th>Email</th>
        <th>Contraseña</th>
        <th>Genero</th>
        <th>Usuario Nuevo</th>
      </tr>
      <tr v-for="user in users" :key="user.email">
        <td>{{ user.name | allCaps }}</td>
        <td>{{ user.email }}</td>
        <td>{{ user.password | censorPassword }}</td>
        <td>{{ user.gender | transformGender }}</td>
        <td>{{ user.isNewUser | transformIsNewUser }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'TableComponent',
  props: {
    users: Array,
  },
  filters: {
    allCaps: function (string) {
      return string.toUpperCase();
    },
    censorPassword: function (string) {
      return string.replace(/./g, '*');
    },
    transformIsNewUser: function (boolean) {
      return boolean ? 'Si' : 'No';
    },
    transformGender: function (string) {
      if (string === 'male') {
        return 'Masculino';
      } else {
        return 'Female';
      }
    },
  },
};
</script>
