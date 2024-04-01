<template>
    <nav class="navbar navbar-expand-md navbar-light bg-light">
      <div class="container">
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item">
              <router-link to="/" class="nav-link">Home</router-link>
            </li>
          </ul>

          <ul class="navbar-nav ms-auto">
            <!-- If the user is authenticated, show the settings dropdown -->
            <li class="nav-item dropdown" v-if="isAuthenticated">
              <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                Settings 
              </a>
              <ul class="dropdown-menu">
                <li>
                  <router-link to="/profile" class="dropdown-item dropdown-profile"> Profile </router-link>
                </li>
                <li>
                  <a class="dropdown-item" @click="logout"> Logout </a>
                </li>
              </ul>
            </li>

            <!-- If the user is not authenticated, show the login button -->
            <li class="nav-item" v-else>
              <a class="button btn-primary" href="#" role="button" @click="login">Login</a>
            </li>
          </ul>
          

        </div>
      </div>
    </nav>
</template>

<script>
import { useAuth0 } from '@auth0/auth0-vue';

export default {
  name: "NavBar",
  setup() {
    const auth0 = useAuth0();
    
    return {
      isAuthenticated: auth0.isAuthenticated,
      isLoading: auth0.isLoading,
      user: auth0.user,
      login() {
        auth0.loginWithRedirect();
      },
      logout() {
        auth0.logout({
          logoutParams: {
            returnTo: window.location.origin
          }
        });
      }
    }
  }
};
</script>

<style>
#mobileAuthNavBar {
  min-height: 125px;
  justify-content: space-between;
}
</style>
