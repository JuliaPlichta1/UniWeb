<template>
  <nav class="navbar sticky-top navbar-expand-md navbar-dark bg-dark">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand">
        <svg xmlns="http://www.w3.org/2000/svg" width="23" height="23" fill="orange" class="bi bi-reddit" viewBox="0 0 17 17">
          <path d="M6.167 8a.831.831 0 0 0-.83.83c0 .459.372.84.83.831a.831.831 0 0 0 0-1.661zm1.843 3.647c.315 0 1.403-.038 1.976-.611a.232.232 0 0 0 0-.306.213.213 0 0 0-.306 0c-.353.363-1.126.487-1.67.487-.545 0-1.308-.124-1.671-.487a.213.213 0 0 0-.306 0 .213.213 0 0 0 0 .306c.564.563 1.652.61 1.977.61zm.992-2.807c0 .458.373.83.831.83.458 0 .83-.381.83-.83a.831.831 0 0 0-1.66 0z"/>
          <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zm-3.828-1.165c-.315 0-.602.124-.812.325-.801-.573-1.9-.945-3.121-.993l.534-2.501 1.738.372a.83.83 0 1 0 .83-.869.83.83 0 0 0-.744.468l-1.938-.41a.203.203 0 0 0-.153.028.186.186 0 0 0-.086.134l-.592 2.788c-1.24.038-2.358.41-3.17.992-.21-.2-.496-.324-.81-.324a1.163 1.163 0 0 0-.478 2.224c-.02.115-.029.23-.029.353 0 1.795 2.091 3.256 4.669 3.256 2.577 0 4.668-1.451 4.668-3.256 0-.114-.01-.238-.029-.353.401-.181.688-.592.688-1.069 0-.65-.525-1.165-1.165-1.165z"/>
        </svg>
        MicroReddit
      </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0 align-items-center">
          <li class="nav-item" v-if="isAuth">
            <router-link to="/userboard" class="nav-link">Userboard</router-link>
          </li>
          <li class="nav-item" v-if="isAuth">
            <router-link to="/subreddits/create" class="nav-link">New subreddit</router-link>
          </li>
          <li class="nav-item" v-if="!isAuth">
            <router-link to="/login" class="nav-link">Login</router-link>
          </li>
          <li class="nav-item" v-if="!isAuth">
            <router-link to="/register" class="nav-link">Register</router-link>
          </li>
          <li class="nav-item" v-if="isAuth">
            <router-link to="/logout" class="nav-link">Logout</router-link>
          </li>
        </ul>
        <form @submit="submit">
          <div class="input-group">
            <select class="input-group-text" v-model="searchType">
              <option selected value="subreddits">Subreddits</option>
              <option value="posts">Posts</option>
            </select>
            <input type="search" class="p-2 form-control" v-model="searchValue" placeholder="Search" aria-label="Search">
            <button class="btn btn-outline-success" type="submit">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-search" viewBox="0 0 16 16">
                <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"/>
              </svg>
            </button>
          </div>
        </form>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapGetters } from 'vuex';
export default {
  name: 'Navbar',
  data() {
    return {
      searchValue: '',
      searchType: 'subreddits',
    };
  },
  computed: {
    ...mapGetters([
      'isAuth',
    ])
  },
  methods: {
    submit(event) {
      event.preventDefault();
      if (this.searchValue !== '') {
        this.$router.push({
          name: 'SearchResults',
          query: { q: this.searchValue, t: this.searchType }
        });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import '@/styles/navbar.scss';
</style>
