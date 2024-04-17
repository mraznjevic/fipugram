<template>
  <div id="app">
    <nav id="nav" class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">
        <img src="@/assets/Sunset-Bar-Logo-300x212.png" width="auto" height="40" class="d-inline-block align-top" alt="" loading="lazy"/>
        Fipugram
      </a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarToggler">
        <form id="search"  class= "navbar-form form-inline ml-auto">
        <input v-model="store.searchTerm" 
        class="form-control mr-sm-2" 
        type="search"
        placeholder="Search" 
        aria-label="Search"/>
        </form>
        <!--Image and text-->
        <ul class="navbar-nav mr-auto mt-2 mt-lg-0">
          <li class="nav-item">
            <router-link to="/" class="nav-link">Home</router-link>
          </li>
          <li v-if="!store.currentUser" class="nav-item">
            <router-link to="/login" class="nav-link">Login</router-link>
          </li>
          <li v-if="!store.currentUser" class="nav-item">
            <router-link to="/signup" class="nav-link">Sign up</router-link>
          </li>
          <li v-if="store.currentUser" class="nav-item">
            <a href="#" @click="logout()" class="nav-link">Logout</a>
          </li>
        </ul>
        <nav class="navbar navbar-light bg-light">
  <form class="form-inline">
  </form>
</nav>
      </div>
    </nav>
    <router-view/>
  </div>
</template>


<script>
import store from '@/store';
import { firebase } from '@/firebase';
import  router  from '@/router';


firebase.auth().onAuthStateChanged((user) => {
 if (user) {
 // User is signed in.
 console.log('*** User', user.email);
 store.currentUser = user.email;
 } else {
 // User is not signed in.
 console.log('*** No user');
 store.currentUser = null;
 if (router.name !== 'login') {
 router.push({ name: 'login' });
 }
 }
});

export default {
  name: 'app',
     data () {
         return{
           store: store, 
         };
      },
      methods:{
        logout(){
          firebase
          .auth()
          .signOut()
          .then (() => {
             this.$router.push({ name: 'login'});
          });
        },
      },
};
</script>

<style>
/* Dodajte prilagodbe CSS-a ovdje ako je potrebno */
</style>



<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
  background-color: white !important;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
