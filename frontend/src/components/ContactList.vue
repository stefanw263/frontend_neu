<script setup>
    defineProps({

        contacts: {
            type: Array,
            required: true
        }

    })
</script>

<template>
    <sui-grid doubling :columns="2">
    <sui-grid-column>
        <sui-input  fluid action="Search" placeholder="Firstname... Lastname..." />
    </sui-grid-column>
    <sui-grid-column>
        <sui-button color="black" @click="createContact()">
            <sui-icon name="add" />
            add new contact
        </sui-button>
    </sui-grid-column>
    </sui-grid>

    <sui-grid class="grid" doubling :columns="4">

      <sui-grid-column v-for="contact in contacts" v-bind:key="contact._id">

        <sui-card>
            
            <sui-image v-if="contact.gender === 'M'" src="/img/male.png" wrapped />
            <sui-image v-else-if="contact.gender === 'F'" src="/img/female.png" wrapped />
            <sui-image v-else src="/img/diverse.png" wrapped />

            <sui-card-content>
                <sui-card-header textAlign="center">{{ contact.firstname }} {{ contact.middlename }} {{ contact.lastname }}</sui-card-header>
            </sui-card-content>

            <sui-card-description textAlign="center">
                <span><sui-icon name="mail" color="black" /> {{ contact.email }}</span> 
                <br />
                <span><sui-icon name="phone" color="black" /> {{ contact.mobile }}</span> 
            </sui-card-description>

            <sui-card-content extra>
                <sui-button-group icon :widths="2">
                    <sui-button color="blue" @click="editContact(contact)"><sui-icon name="edit" /></sui-button>
                    <sui-button color="red" @click="deleteContact(contact._id)"><sui-icon name="delete" /></sui-button>
                </sui-button-group>
            </sui-card-content>
        </sui-card>

      </sui-grid-column>

    </sui-grid>
</template>

<script>
    export default {
        methods: {
            async deleteContact(id) {
                try {
                    let response = await fetch(`http://localhost:3000/contacts/${id}`, {
                        method: "DELETE"
                    })
                    const res = await response.json()
                    this.$emit('showEvent')
                } catch (error) {
                    console.log(error)
                }
            },
            editContact(contact){
                this.$emit('editEvent', contact)
            },
            createContact(){
                this.$emit('createEvent')
            }
        }
    }
</script>