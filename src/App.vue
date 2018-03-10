<template>
  <div class="app">
    <AppHeader :title="title" :subtitle="subtitle"/>
    <section class="Cards">
      <UserCard :users="users" :user="user" v-for="(user, key) in users" :key="key" />
    </section>
    <AppFooter :copyright="copyright"/>
  </div>
</template>

<script>
import Axios from "axios";
import AppHeader from "./components/Header";
import UserCard from "./components/UserCard";
import AppFooter from "./components/Footer";

export default {
  name: "app",
  components: {
    AppHeader,
    UserCard,
    AppFooter
  },
  mounted() {
    Axios.get(
      "https://randomuser.me/api/?results=12&inc=name,picture,dob,location,phone&nat=us"
    ).then(res => {
      let all = res.data.results;
      let us = [];
      let u = {};

      for (let i = 0; i < all.length; i++) {
        u = {
          photo: all[i].picture.large,
          fullName: all[i].name.first + " " + all[i].name.last,
          birthday: all[i].dob.split(" ", 1).toString(),
          address: all[i].location.street,
          phone: all[i].phone
        };
        us.push(u);
      }
      this.users = us;
    });
  },
  data() {
    return {
      title: "Chris Med | Vue-App",
      subtitle: "Random User Cards",
      copyright: "Christian Medina | Copyright 2018",
      users: []
    };
  }
};
</script>

<style lang="scss">
.app {
  width: 100%;
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 300px 1fr 100px;
}

.Cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, 320px);
  grid-gap: 1.5rem;
  justify-content: center;
  width: 90%;
  max-width: 1200px;
  margin: -50px auto 50px;
}
</style>
