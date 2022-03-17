<template>
  <div class="container">
    <h2>Asistencia</h2>
    <div class="row justify-content-center">
      <form class="col-6" @submit.prevent="checkForm">
        <div class="alert alert-danger" role="alert" v-if="errors.length">
          <b>Corrige los siguientes errores:</b>
          <ul>
            <li v-for="error in errors" :key="error">{{ error }}</li>
          </ul>
        </div>
        <div class="form-outline mb-4">
          <label class="form-label" for="name">Nombre completo</label>
          <input type="text" id="name" class="form-control" v-model="name" />
        </div>

        <div class="form-outline mb-4">
          <label class="form-label" for="email">Email</label>
          <input type="email" id="email" class="form-control" v-model="email" />
        </div>

        <div class="form-outline mb-4">
          <label class="form-label" for="password">Contraseña</label>
          <input
            type="password"
            id="password"
            class="form-control"
            v-model="password"
          />
        </div>

        <div class="form-outline mb-4">
          <label class="form-label" for="password2">Repetir contraseña</label>
          <input
            type="password"
            id="password2"
            class="form-control"
            v-model="password2"
          />
        </div>

        <div class="row mb-4">
          <h4 class="col-6">Genero</h4>
          <div class="col-6 d-flex justify-content-center">
            <div class="form-check">
              <input
                type="radio"
                id="male"
                class="form-check-input"
                name="gender"
                value="male"
                v-model="gender"
              />
              <label for="male">Masculino</label> <br />
              <input
                type="radio"
                id="female"
                class="form-check-input"
                name="gender"
                value="female"
                v-model="gender"
              />
              <label for="female">Femenino</label>
            </div>
          </div>
        </div>

        <div class="row mb-4">
          <div class="col d-flex justify-content-center">
            <div class="form-check">
              <input
                type="checkbox"
                id="isNewUser"
                class="form-check-input"
                v-model="isNewUser"
              />
              <label class="form-check-label" for="isNewUser">
                ¿Es nuevo usuario?
              </label>
            </div>
          </div>
        </div>

        <button type="submit" class="btn btn-primary btn-block">
          Agregar usuario
        </button>
        <button @click="emptyTable" class="btn btn-danger btn-block">
          Vaciar tabla
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FormComponent',
  props: {
    addUser: Function,
    emptyTable: Function,
  },
  data: function () {
    return {
      name: null,
      email: null,
      password: null,
      password2: null,
      isNewUser: false,
      gender: null,
      errors: [],
    };
  },

  methods: {
    validEmail: function (email) {
      const regex =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return regex.test(email);
    },
    passwordMatch: function (password, password2) {
      return password === password2;
    },
    checkForm: function () {
      this.errors = [];
      if (!this.name) {
        this.errors.push('El nombre es requerido');
      } else if (!this.validEmail(this.email)) {
        this.errors.push('El email es inválido');
      } else if (!this.password) {
        this.errors.push('La contraseña es requerida');
      } else if (!this.passwordMatch(this.password, this.password2)) {
        this.errors.push('Las contraseñas no coinciden');
      } else if (!this.gender) {
        this.errors.push('Debes seleccionar un genero');
      } else {
        const user = {
          name: this.name,
          email: this.email,
          password: this.password,
          gender: this.gender,
          isNewUser: this.isNewUser,
        };
        (this.errors = []),
          (this.name = null),
          (this.email = null),
          (this.password = null),
          (this.password2 = null),
          (this.gender = null),
          (this.isAccepted = false);
        this.addUser(user);
      }
    },
  },
};
</script>
