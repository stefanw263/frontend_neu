<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <sui-menu fixed>
        <sui-menu-item>
          
        <RouterLink to="/">
          <sui-button color="orange">    
            Welcome
          </sui-button>
          
        </RouterLink>
        </sui-menu-item>
        <sui-menu-item v-if="authenticated">
          <sui-button color="green" @click="showContact()">    
            Contact List
          </sui-button>
        </sui-menu-item>
        <sui-menu-menu position="right">
            <sui-menu-item>
                <RouterLink v-if="!authenticated" to="/login">
                    <sui-button color="orange">    
                        Login
                    </sui-button>
                </RouterLink>
                <RouterLink v-else to="/login" @click.native="logout()" replace>
                    <sui-button color="orange">    
                        Logout
                    </sui-button>
                </RouterLink>
            </sui-menu-item>
        </sui-menu-menu>
    </sui-menu>
  </header>

  <main>

    <RouterView @authenticated="setAuthenticated" :auth="authenticated" />
  </main>

</template>

<style>
main {
  margin: 100px 10vw;
}
</style>


<script>
    export default {
        name: 'App',
        data() {
            return {
                authenticated: false
            }
        },
        methods: {
            setAuthenticated(status) {
                this.authenticated = status;
            },
            logout() {
                this.authenticated = false;
            },
            showContact(){
              this.$router.replace({ name: "contacts" })
            },
            showStart(){
              this.$router.replace({ name: "hello" })
            }
        }
    }
</script>