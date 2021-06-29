<template>
  <div id="app">
    <div class="top" v-if="showTable">
      <input
        type="search"
        placeholder="Search user by last nmae"
        v-model="search"
      />
      <button @click="showUserForm" style="margin-left: 1vw">Add user</button>
    </div>

    <div v-if="showForm">
      <form @submit="adduser" class="form-style-9" v-if="!isEditUser">
        <label for="fname">First name:</label><br />
        <input
          type="text"
          v-model="newUser.firstName"
          placeholder="Enter your first name"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Last name:</label><br />
        <input
          type="text"
          v-model="newUser.lastName"
          placeholder="Enter your Last name"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Date of Birth:</label><br />
        <input
          type="date"
          max="2021-06-29"
          v-model="newUser.dateofbirth"
          placeholder="Enter your Date of Birth"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Address:</label><br />
        <input
          type="text"
          v-model="newUser.address"
          placeholder="Enter your Address"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Phone Number:</label><br />
        <input
          type="number"
          v-model="newUser.phone"
          placeholder="Enter your Phone"
          class="field-style field-split align-left"
          required
        /><br />
        <input type="submit" value="Submit" />
      </form>
      <form @submit="updateuser" class="form-style-9" v-if="isEditUser">
        <label for="fname">First name:</label><br />
        <input
          type="text"
          v-model="newUser.firstName"
          placeholder="Enter your first name"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Last name:</label><br />
        <input
          type="text"
          v-model="newUser.lastName"
          placeholder="Enter your Last name"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Date of Birth:</label><br />
        <input
          type="date"
          max="2021-06-29"
          v-model="newUser.dateofbirth"
          placeholder="Enter your Date of Birth"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Address:</label><br />
        <input
          type="text"
          v-model="newUser.address"
          placeholder="Enter your Address"
          class="field-style field-split align-left"
          required
        /><br />
        <label for="lname">Phone Number:</label><br />
        <input
          type="number"
          v-model="newUser.phone"
          placeholder="Enter your Phone"
          class="field-style field-split align-left"
          required
        /><br />
        <input type="submit" value="Submit" />
      </form>
    </div>
    <div v-if="showTable">
      <ul class="responsive-table">
        <li class="table-header">
          <div class="col col-1">No</div>
          <div class="col col-2">First Name</div>
          <div class="col col-2">Last Name</div>
          <div class="col col-2">Date of Birth</div>
          <div class="col col-4">Address</div>
          <div class="col col-2">Phone</div>
          <div class="col col-2">Edit/Delete</div>
        </li>
        <li
          class="table-row"
          v-for="(user, index) in searchedUser"
          :key="index"
        >
          <div class="col col-1">{{ index + 1 }}</div>
          <div class="col col-2">{{ user.firstName }}</div>
          <div class="col col-2">{{ user.lastName }}</div>
          <div class="col col-2">{{ user.dateofbirth }}</div>
          <div class="col col-4">{{ user.address }}</div>
          <div class="col col-2">{{ user.phone }}</div>
          <div class="col col-2">
            <button @click="edit(user.id)">edit</button>
            <button @click="remove(user.id)">delete</button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      showForm: false,
      showTable: true,
      isEditUser: false,
      users: [],
      search: "",
      newUser: {
        firstName: "",
        lastName: "",
        dateofbirth: "",
        address: "",
        phone: "",
      },
    };
  },
  computed: {
    searchedUser() {
      if (this.search.trim() === "") {
        return this.users;
      } else {
        return this.users.filter((user) => {
          return user.lname.includes(this.search);
        });
      }
    },
  },
  methods: {
    adduser(e) {
      e.preventDefault();
      this.users.push(this.newUser);
      this.showUsersTable();
    },
    showUserForm() {
      this.showForm = true;
      this.showTable = false;
    },
    showUsersTable() {
      this.showForm = false;
      this.showTable = true;
    },
    remove(id) {
      let list = [];
      this.users.forEach((user) => {
        if (user.id !== id) {
          list.push(user);
        }
      });
      this.users = list;
    },
    edit(id) {
      let targetUser = this.users.find((user) => {
        return user.id === id;
      });
      this.isEditUser = true;
      this.newUser = targetUser;
      this.showUserForm();
    },
    updateuser(e) {
      e.preventDefault();
      let list = this.users.map((user) => {
        if (user.id === this.newUser.id) {
          return this.newUser;
        } else {
          user;
        }
      });
      this.users = list;
      this.isEditUser = false;
      this.newUser = {
        firstName: "",
        LastName: "",
        dateofbirth: "",
        address: "",
        phone: "",
      };
      this.showUsersTable();
    },
  },
};
</script>

<style>
body {
  font-family: "lato", sans-serif;
}
.container {
  max-width: 1000px;
  margin-left: auto;
  margin-right: auto;
  padding: 10px;
}
h2 {
  font-size: 26px;
  margin: 20px 0;
  text-align: center;
}
h2 small {
  font-size: 0.5em;
}
.responsive-table li {
  border-radius: 3px;
  padding: 25px 30px;
  display: flex;
  justify-content: space-between;
  margin-bottom: 25px;
}
.responsive-table .table-header {
  background-color: #95a5a6;
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}
.responsive-table .table-row {
  background-color: #fff;
  box-shadow: 0px 0px 9px 0px rgba(0, 0, 0, 0.1);
}
.responsive-table .col-1 {
  flex-basis: 10%;
}
.responsive-table .col-2 {
  flex-basis: 40%;
}
.responsive-table .col-3 {
  flex-basis: 25%;
}
.responsive-table .col-4 {
  flex-basis: 25%;
}
@media all and (max-width: 767px) {
  .responsive-table .table-header {
    display: none;
  }
  .responsive-table li {
    display: block;
  }
  .responsive-table .col {
    flex-basis: 100%;
  }
  .responsive-table .col {
    display: flex;
    padding: 10px 0;
  }
  .responsive-table .col:before {
    color: #6c7a89;
    padding-right: 10px;
    content: attr(data-label);
    flex-basis: 50%;
    text-align: right;
  }
}

.top {
  display: flex;
  min-width: 90%;
  flex-direction: row;
  justify-content: flex-end;
}

.form-style-9 {
  max-width: 450px;
  background: #fafafa;
  padding: 30px;
  margin: 50px auto;
  box-shadow: 1px 1px 25px rgba(0, 0, 0, 0.35);
  border-radius: 10px;
  border: 6px solid #305a72;
}
.form-style-9 ul {
  padding: 0;
  margin: 0;
  list-style: none;
}
.form-style-9 ul li {
  display: block;
  margin-bottom: 10px;
  min-height: 35px;
}
.form-style-9 ul li .field-style {
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  padding: 8px;
  outline: none;
  border: 1px solid #b0cfe0;
  -webkit-transition: all 0.3s ease-in-out;
  -moz-transition: all 0.3s ease-in-out;
  -ms-transition: all 0.3s ease-in-out;
  -o-transition: all 0.3s ease-in-out;
}
.form-style-9 ul li .field-style:focus {
  box-shadow: 0 0 5px #b0cfe0;
  border: 1px solid #b0cfe0;
}
.form-style-9 ul li .field-split {
  width: 49%;
}
.form-style-9 ul li .field-full {
  width: 100%;
}
.form-style-9 ul li input.align-left {
  float: left;
}
.form-style-9 ul li input.align-right {
  float: right;
}
.form-style-9 ul li textarea {
  width: 100%;
  height: 100px;
}
.form-style-9 ul li input[type="button"],
.form-style-9 ul li input[type="submit"] {
  -moz-box-shadow: inset 0px 1px 0px 0px #3985b1;
  -webkit-box-shadow: inset 0px 1px 0px 0px #3985b1;
  box-shadow: inset 0px 1px 0px 0px #3985b1;
  background-color: #216288;
  border: 1px solid #17445e;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  padding: 8px 18px;
  text-decoration: none;
  font: 12px Arial, Helvetica, sans-serif;
}
.form-style-9 ul li input[type="button"]:hover,
.form-style-9 ul li input[type="submit"]:hover {
  background: linear-gradient(to bottom, #2d77a2 5%, #337da8 100%);
  background-color: #28739e;
}
label {
  margin-top: 0.5vh;
}
input {
  margin-top: 1vh;
}
</style>
