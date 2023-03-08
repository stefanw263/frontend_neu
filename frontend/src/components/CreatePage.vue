<template>

    <sui-header as="h1" textAlign="center">Create new Contact</sui-header>

    <sui-form id="contact-form" @submit="checkForm">
        <sui-form-group action="">
            <sui-grid :columns="2" divided>
                <sui-grid-row>
                    <sui-grid-column>
                        <div class="field">
                            <label>First Name</label>
                            <sui-input
                                placeholder="John"
                                v-model="firstname"
                            />
                        </div>
                    </sui-grid-column>
                    <sui-grid-column>
                        <div class="field">
                            <label>Last Name</label>
                            <sui-input
                                placeholder="Doe"
                                v-model="lastname"
                            />
                        </div>
                    </sui-grid-column>
                </sui-grid-row>

                <sui-grid-row>
                    <sui-grid-column>
                        <div class="field">
                            <label>Middle Name</label>
                            <sui-input
                                placeholder="Jane"
                                v-model="middlename"
                            />
                        </div>
                    </sui-grid-column>
                    <sui-grid-column>
                        <div class="field">
                            <label>Gender</label>
                            <sui-dropdown
                                selection
                                placeholder="Gender"
                                v-model="gender"
                                :options="['M', 'F', 'D']"
                            />
                        </div>
                    </sui-grid-column>
                </sui-grid-row>

                <sui-grid-row>
                    <sui-grid-column>
                        <div class="field">
                            <label>E-Mail</label>
                            <sui-input
                                placeholder="john@doe.com"
                                v-model="email"
                            />
                        </div>
                    </sui-grid-column>
                    <sui-grid-column>
                        <div class="field">
                            <label>Phone</label>
                            <sui-input
                                placeholder="0123124244"
                                v-model="mobile"
                            />
                        </div>
                    </sui-grid-column>
                </sui-grid-row>

                <sui-grid-row>
                    <sui-grid-column>
                        <sui-button color="green" type="button" @click="createContact">
                            <sui-icon name="check" />
                            Submit
                        </sui-button>
                    </sui-grid-column>
                    <sui-grid-column>
                        <sui-button color="red" type="button">
                            <sui-icon name="cancel" />
                            Cancel
                        </sui-button>
                    </sui-grid-column>
                </sui-grid-row>
            </sui-grid>
        </sui-form-group>
    </sui-form>
</template>

<script>
    export default {

        data() {
            return {
                firstname: '',
                lastname: '',
                middlename: '',
                gender: '',
                email: '',
                mobile: ''
            }
        },
        
        methods: {
            
            async createContact() {
                console.log(this.firstname)

                try {
                    const data = {
                        "firstname" : this.firstname,
                        "lastname" : this.lastname,
                        "middlename" : this.middlename,
                        "gender" : this.gender,
                        "email" : this.email,
                        "mobile" : this.mobile
                    }

                    let response = await fetch('http://localhost:3000/contacts/', {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json",
                         },
                        body: JSON.stringify(data)
                    })

                    const res = await response.json()

                    if(res.acknowledged){
                        this.$emit('showEvent')
                    }

                } catch (error) {
                    console.log(error)
                }
            },

        }
    }
</script>