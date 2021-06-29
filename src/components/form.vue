<template>
  <section class="form">
    <form @submit="addUser">
      <label for="fname">First name:</label><br />
      <input
        type="text"
        v-model="user.fname"
        placeholder="Enter your first name"
        required
      /><br />
      <label for="lname">Last name:</label><br />
      <input
        type="text"
        v-model="user.lname"
        placeholder="Enter your Last name"
        required
      /><br />
      <label for="lname">Date of Birth:</label><br />
      <input
        type="date"
        max="2021-06-29"
        v-model="user.dob"
        placeholder="Enter your Date of Birth"
        required
      /><br />
      <label for="lname">Address:</label><br />
      <input
        type="text"
        v-model="user.address"
        placeholder="Enter your Address"
        required
      /><br />
      <label for="lname">Phone Number:</label><br />
      <input
        type="number"
        v-model="user.phone"
        placeholder="Enter your Phone"
        required
      /><br />
      <input
        type="submit"
        :value="action === 'new' ? 'Add New User' : 'Update User'"
      />
    </form>
  </section>
</template>

<script>
export default {
  props: {
    action: {
      type: String,
      required: true,
    },
    currentUser: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      user: {
        fname: "",
        lname: "",
        dob: "",
        address: "",
        phone: "",
      },
    };
  },
  methods: {
    addUser(e) {
      e.preventDefault();
      if (this.action === "new") {
        this.user.id = Date.now();
        this.$emit("newUser", this.user);
      } else {
        this.$emit("updateUser", this.user);
      }
    },
  },
  mounted() {
    if (this.action === "edit") {
      this.user = this.currentUser;
    }
  },
};
</script>

<style>
input[type="text"],
input[type="number"],
input[type="date"],
select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input[type="submit"] {
  width: 100%;
  background-color: #4caf50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type="submit"]:hover {
  background-color: #45a049;
}
</style>