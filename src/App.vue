<template>
  <div id="app">
    <div class="row__end" v-if="currenctComponent == 'table'">
      <input
        type="Search user by last nmae"
        v-model="search"
        v-if="userList.length > 0"
      />
      <button @click="showUserForm">Add user</button>
    </div>
    <tableComponent
      v-if="currenctComponent === 'table'"
      :filteredUsers="filteredUsers"
      @edituser="edituser"
      @removeuser="removeuser"
    />
    <formComponent
      v-if="currenctComponent === 'form'"
      :action="action"
      :currentUser="currentUser"
      @newUser="addUserToTable"
      @updateUser="updateUser"
    />
  </div>
</template>

<script>
import tableComponent from "./components/table.vue";
import formComponent from "./components/form.vue";

export default {
  name: "App",
  components: {
    tableComponent,
    formComponent,
  },
  data() {
    return {
      currenctComponent: "table",
      action: "new",
      userList: [],
      currentUser: {},
      search: "",
    };
  },
  computed: {
    filteredUsers() {
      if (this.search.trim() === "") {
        return this.userList;
      } else {
        return this.userList.filter((user) => {
          return user.lname.toLowerCase().includes(this.search.toLowerCase());
        });
      }
    },
  },
  methods: {
    addUserToTable(user) {
      this.userList.push(user);
      this.currenctComponent = "table";
    },
    showUserForm() {
      this.currenctComponent = "form";
    },
    removeuser(id) {
      let updated_users = [];
      this.userList.forEach((user) => {
        if (user.id !== id) {
          updated_users.push(user);
        }
      });
      this.userList = updated_users;
    },
    edituser(id) {
      this.currentUser = this.userList.find((user) => {
        return user.id === id;
      });
      this.action = "edit";
      this.currenctComponent = "form";
    },
    updateUser(updatedUser) {
      let updated_users = this.userList.map((user) => {
        if (user.id === updatedUser.id) {
          return updatedUser;
        } else {
          user;
        }
      });
      this.userList = updated_users;
      this.action = "new";
      this.currentUser = Object.assign({}, {});
      this.currenctComponent = "table";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}
div {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}
.row__end {
  display: flex;
  min-width: 90%;
  flex-direction: row;
  justify-content: flex-end;
}
button {
  margin-left: 1vw;
}
</style>
