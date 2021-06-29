<template>
  <div>
    <table>
      <tr>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Date of Birth</th>
        <th>Address</th>
        <th>Contact Number</th>
        <th>Action</th>
      </tr>
      <tr v-for="(user, index) in filteredUsers" :key="index">
        <td>{{ user.fname }}</td>
        <td>{{ user.lname }}</td>
        <td>{{ user.dob }}</td>
        <td>{{ user.address }}</td>
        <td>{{ user.phone }}</td>
        <td>
          <button class="edit" @click="editUser(user.id)">edit</button>
          <button class="delete" @click="deleteUser(user.id)">delete</button>
        </td>
      </tr>
      <tr v-if="filteredUsers.length === 0">
        <td colspan="6">No User Found, Please add users first</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    filteredUsers: {
      type: Array,
      required: true,
    },
  },
  methods: {
    deleteUser(id) {
      this.$emit("removeuser", id);
    },
    editUser(id) {
      this.$emit("edituser", id);
    },
  },
};
</script>

<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
.edit {
  background-color: blue;
  border-color: blue;
  color: white;
}
.delete {
  background-color: red;
  border-color: red;
  margin-left: 1vw;
  color: white;
}
</style>