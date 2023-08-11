<script>
export default {
  data() {
    return {
      name: "Nome",
      login: "Login",
      company: "Empresa",
      bio: "...",
      avatar_url: "https://unsplash.it/256",
      searchInput: "",
    };
  },

  methods: {
    async fetchGithubUser() {
      const res = await fetch(
        `https://api.github.com/users/${this.searchInput}`
      );
      const { login, name, company, bio, avatar_url } = await res.json();

      this.login = login;
      this.name = name;
      this.bio = bio;
      this.company = company;
      this.avatar_url = avatar_url;
    },
  },
};
</script>

<template>
  <h2>GitHub User Data</h2>
        <input type="text" v-model="searchInput">
        <button v-on:click="fetchGithubUser">Carregar Usuário</button>
        <img v-bind:src="avatar_url">
        <strong>@{{ login }}</strong>
        <h1>{{ name }}</h1>
        <h2>{{ company }}</h2>
        <span>{{ bio }}</span>
</template>
