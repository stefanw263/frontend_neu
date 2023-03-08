<script setup>

import ContactList from '../components/ContactList.vue'

</script>

<template>
  <div v-if="content === 1">
      <EditPage @show-event="show" :contact="editContact"></EditPage>
    </div>

    <div v-else-if="content === 2">
      <CreatePage @show-event="show"></CreatePage>
    </div>

    <div v-else>
      <ContactList @show-event="show" @edit-event="edit" @create-event="create" :contacts="contacts"></ContactList>
    </div>
</template>

<script>
    export default {
        name: 'Home',
        props: ['auth'],
        data() {
          return {
            contacts: [],
            editContact: null,
            content: 0
          }
        },
        mounted() {
            if(!this.auth) {
                this.$router.replace({ name: "login" });
            }
        },
        created(){
          this.getData()
        },
        methods: {
          async getData() {
            try {
              let response = await fetch("http://localhost:3000/contacts", {
                method: "GET"
              })
              this.contacts = await response.json()
            } catch (error) {
              console.log(error)
            }
          },
          edit(contact){
            this.editContact = contact
            console.log(contact)
            console.log(this.editContact)
            this.content = 1
          },
          create(){
            this.content = 2
          },
          show(){
            this.getData()
            this.content = 0
          },
        },
    }
</script>
