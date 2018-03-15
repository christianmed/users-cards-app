<template>
  <div class="app">
    <AppHeader :title="title" :subtitle="subtitle"/>
    <input v-model="search" class="search" type="text" placeholder="Search User by Name">
    <section class="Cards">
      <UserCard :user="user" v-for="(user, key) in filteredByName" :key="key" />
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
    // Axios.get(
    //   "https://randomuser.me/api/?results=120&inc=name,picture,dob,location,phone&nat=us"
    // ).then(res => {
    //   let all = res.data.results;
    //   let us = [];
    //   let u = {};

    //   for (let i = 0; i < all.length; i++) {
    //     u = {
    //       photo: all[i].picture.large,
    //       fullName: all[i].name.first + " " + all[i].name.last,
    //       birthday: all[i].dob.split(" ", 1).toString(),
    //       address: all[i].location.street,
    //       phone: all[i].phone
    //     };
    //     us.push(u);
    //   }
    //   this.users = us;
    // });
    Axios.get(
      "https://randomuser.me/api/?results=120&inc=name,picture,dob,location,phone&nat=us"
    ).then(res => {
      console.log(res.data.results);
      const array = res.data.results.map(user => {
        return {
          fullName: `${user.name.first} ${user.name.last}`,
          birthday: user.dob.split(" ", 1).toString(),
          address: user.location.state,
          phone: user.phone,
          photo: user.picture.large
        };
      });
      this.users = array;
    });
  },
  data() {
    return {
      title: "Chris Med | Vue-App",
      subtitle: "Random User Cards",
      copyright: "Christian Medina | Copyright 2018",
      users: [],
      search: ""
    };
  },
  computed: {
    filteredByName() {
      return this.users.filter(user => {
        return user.fullName.includes(this.search);
      });
    }
  }
};
</script>

<style lang="scss">
@import "./scss/styles.scss";

.app {
  width: 100%;
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 150px 60px 1fr 100px;
  grid-gap: 2rem;
}

.search {
  display: block;
  width: 90%;
  max-width: 1200px;
  margin: 0 auto 0;
  padding: 0 1rem;
  font-size: 1rem;
  border: 0;
  outline: 0;
  border: 1px solid rgba(map-get($vars, accent), 0.75);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
}

.Cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 340px));
  grid-gap: 1.5rem;
  justify-content: center;
  width: 90%;
  max-width: 1200px;
  margin: 0 auto 0;
}
</style>
