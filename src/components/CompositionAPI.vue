<script setup>
import { reactive } from "vue";

const state = reactive({
  name: "Nome",
  login: "Login",
  company: "Empresa",
  bio: "...",
  avatar_url: "https://unsplash.it/256",
  searchInput: "",
});

async function fetchGithubUser() {
  const res = await fetch(`https://api.github.com/users/${state.searchInput}`);
  const { login, name, company, bio, avatar_url } = await res.json();

  state.login = login;
  state.name = name;
  state.bio = bio;
  state.company = company;
  state.avatar_url = avatar_url;
}
</script>
 
<template>
    <h1>GitHub User Data</h1>
        <input type="text" v-model="state.searchInput">
        <button v-on:click="fetchGithubUser">Carregar Usuário</button>
        <img v-bind:src="state.avatar_url">
        <strong>@{{ state.login }}</strong>
        <h1>{{ state.name }}</h1>
        <h2>{{ state.company }}</h2>
        <span>{{ state.bio }}</span>
</template>