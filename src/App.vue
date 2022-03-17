<template>
  <div id="app">
    <FormComponent :addUser="addUser" :emptyTable="emptyTable" />
    <TableComponent :users="users" />
  </div>
</template>

<script>
import TableComponent from './components/TableComponent.vue';
import FormComponent from './components/FormComponent.vue';

export default {
  name: 'App',
  components: {
    TableComponent,
    FormComponent,
  },
  data: function () {
    return {
      users: [],
    };
  },
  methods: {
    addUser: function (user) {
      this.users.push(user);
    },
    emptyTable: function () {
      this.users = [];
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
