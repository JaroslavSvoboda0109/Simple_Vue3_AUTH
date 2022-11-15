<template>
  <div id="app">
    <nav class="navbar navbar-expand navbar-dark bg-dark">
      <div class="navbar-brand">
        <router-link to="/" class="nav-link" style="color: white;">
          Sherpa
        </router-link>
      </div>
      <div v-if="!currentUser" class="navbar-nav ml-auto">
        <li class="nav-item">
          <router-link to="/login" class="nav-link btn-log-in" style="margin-right: 10px;">
            Se connecter
          </router-link>
        </li>
        <li class="nav-item">
          <router-link to="/register" class="nav-link btn-log-in">
            Inscription
          </router-link>
        </li>
      </div>

      <div v-if="currentUser" class="navbar-nav ml-auto">
        <div class="dropdown">
          <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            {{ currentUser.username }}
          </button>
          <div class="dropdown-menu" aria-labelledby="dropdownMenuButton" style="min-width: auto;">
            <a class="dropdown-item" style="padding: 0.25rem 0.8rem;" @click.prevent="logOut">LogOut</a>
          </div>
        </div>
      </div>
    </nav>

    <router-view />
  </div>
</template>

<script>
export default {
  computed: {
    currentUser() {
      return this.$store.state.auth.user;
    },
    showAdminBoard() {
      if (this.currentUser && this.currentUser["roles"]) {
        return this.currentUser["roles"].includes("ROLE_ADMIN");
      }

      return false;
    },
    showModeratorBoard() {
      if (this.currentUser && this.currentUser["roles"]) {
        return this.currentUser["roles"].includes("ROLE_MODERATOR");
      }

      return false;
    },
  },
  methods: {
    logOut() {
      this.$store.dispatch("auth/logout");
      this.$router.push("/");
    },
  },
};
</script>
<style>
.btn-log-in {
  background-color: white;
  color: black !important;
  border-radius: 25px;
  padding: 3px 22px !important;
}
.btn-log-in:hover {
  color: white !important;
  background-color: #2fcdff;
}
</style>
