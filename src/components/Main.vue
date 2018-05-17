<template lang="pug">
	div.Page
		b-navbar.Menu(toggleable="md" type="dark" variant="dark")
			b-navbar-brand(href="#") Title
			b-navbar-toggle(target="nav_collapse")
			b-collapse(is-nav id="nav_collapse")
				b-navbar-nav
					b-nav-item(v-for="item in menu" :to="item.href" :key="item.href") {{ item.name }}
			b-navbar-nav
				b-nav-item(to="user") {{ username }}
				b-nav-item(@click="logout") Logout
		div.Context
			b-table.Users(hover :fields="users.fields" :items="users.list")
				template(slot="id" slot-scope="data")
					b-button.UserAction(size="sm" variant="primary" @click="edit(data.value)") Edit
					b-button.UserAction(size="sm" variant="danger" @click="remove(data.value)") Delete
</template>

<script>
const data = {
  username: localStorage.login,
  menu: [
    {
      href: "page1",
      name: "page 1"
    },
    {
      href: "page2",
      name: "page 2"
    },
    {
      href: "page3",
      name: "page 3"
    },
    {
      href: "page4",
      name: "page 4"
    }
  ],
  users: {
    fields: {
      name: "Name",
      email: "E-mail",
      phone: "Phone number",
      status: "Status",
      balance: "Balance",
      id: "Actions"
    },
    list: [
      {
        name: "Test User",
        email: "user1@example.com",
        phone: "+79999999999",
        status: "Confirmed",
        balance: (123.4).toFixed(2),
        id: 1
      },
      {
        name: "Test User2",
        email: "user2@example.com",
        phone: "+79999999999",
        status: "Confirmed",
        balance: (234).toFixed(2),
        id: 2
      },
      {
        name: "Test User3",
        email: "user3@example.com",
        phone: "+79999999999",
        status: "Confirmed",
        balance: (0.97).toFixed(2),
        id: 3
      },
      {
        name: "Test User4",
        email: "user4@example.com",
        phone: "+79999999999",
        status: "Confirmed",
        balance: (4966).toFixed(2),
        id: 4
      },
      {
        name: "Test User5",
        email: "user5@example.com",
        phone: "+79999999999",
        status: "Confirmed",
        balance: (0).toFixed(2),
        id: 5
      }
    ]
  }
};

export default {
  name: "Main",
  data() {
    return data;
  },
  methods: {
    logout() {
      delete localStorage.login;

      this.$router.push("login");
    },
    edit(id) {
      alert(`edit user ${id}`);
    },
    remove(id) {
      alert(`delete user ${id}`);
    }
  }
};
</script>

<style scoped>
.Users {
  margin-top: 40px;
}

.UserAction {
  margin: 0 2px;
}
</style>
