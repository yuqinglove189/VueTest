<template>
  <div class="users">
    <h1>Users</h1>
    <!-- 添加用户信息 -->
    <form @submit="addUser">
      <input type="text" v-model="newUser.name" placeholder="enter name">
      <input type="text" v-model="newUser.email" placeholder="enter email">
      <input type="submit" value="Submit">
    </form>
    <!-- 展示用户信息 -->
    <ul>
      <li v-for="user in users">
        <input type="checkbox" class="toggle" v-model="user.contacted">
        <span :class="{contacted:user.contacted}">
          {{user.name}} : {{ user.email}}
          <button @click="deleteUser(user)">X</button>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'users',
    data() {
      return {
        newUser: {},
        users: [
          {
            name: 'Hemiah Wu',
            email: 'hemiah@gmail.com',
            contacted: false
          },
          {
            name: 'Henry Wu',
            email: 'henry@gmail.com',
            contacted: false
          },
          {
            name: 'Emily Wu',
            email: 'emily@gmail.com',
            contacted: false
          },
        ],
      }
    },
    created(){
      this.$http.get("http://jsonplaceholder.typicode.com/users").then(function (response) {
        this.users = response.data;
      })
    },
    methods: {
      addUser() {
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        });
      },
      deleteUser(user) {
        this.users.splice(this.users.indexOf(user), 1);
      }
    },
  }
</script>

<style scoped>
  .contacted {
    text-decoration: line-through;
  }
</style>
