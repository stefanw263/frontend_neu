<script setup>
  
</script>

<template>
  <main>
    Liste...
    <div v-if="auth">
      eingeloggt
    </div>
    <div v-else>
      ausgeloggt
    </div>
  </main>
</template>

<script>
    export default {
        name: 'Home',
        props: ['auth'],
        data() {
          return {}
        },
        mounted() {
            if(!this.auth) {
                this.$router.replace({ name: "login" });
            }
        },
        methods: {
        },
    }
</script>
