<template>
  <div>
    <input type="text" v-model="firstName" />
    <input type="text" v-model="lastName" />
    <span
       v-for="(phone, index) in phones"
       :key="index"
    >
      <input
          v-model="phone.value"
          type="number"
      />
      <button
          v-if="index > 0"
          @click="removePhone(index)"
      >-</button>
    </span>

    <button @click="addPhone">+</button>
    <button @click="addUser">addUser</button>


    <div
        v-for="(user, index) in users"
        :key="index"
    >
      <div>{{user.firstName}}</div>
      <div>{{user.lastName}}</div>
      <div
          v-for="(phone, index) in user.phones"
          :key="index"
      >{{ phone.value }}
      </div>
      <button @click="removeUser(index)">remove user</button>
    </div>

  </div>
</template>

<script>

import usersDB from "@/db/users";

export default {
  name: 'HelloWorld',
  data: function () {
    return {
      users: [],
      firstName: '',
      lastName: '',
      phones: [{
        value: '',
      }]
    }
  },
  created() {
    this.getUsers();
  },
  methods: {
    addPhone() {
      this.phones.push({
        value: ''
      });
    },
    removePhone(index) {
      this.phones.splice(index, 1);
    },
    addUser() {
      const user = {
        firstName: this.firstName,
        lastName: this.lastName,
        phones: this.phones,
      };

      this.users.push(user);
      this.firstName = '';
      this.lastName = '';
      this.phones = [{value: ''}];
    },
    getUsers() {
      setTimeout(() => this.users = usersDB, 1000);
    },
    removeUser(index) {
      this.users.splice(index, 1);
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
