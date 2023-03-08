<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <sui-menu fixed>
        <sui-menu-item as="div">Welcome</sui-menu-item>
        <sui-menu-item v-if="authenticated">
            <sui-button color="orange" @click="showContact()">    
            show Contact List
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

  

  <RouterView @authenticated="setAuthenticated" :auth="authenticated" />
</template>


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
            }
        }
    }
</script>