<template>

    <sui-header as="h1" textAlign="center">Create new Contact</sui-header>

    <sui-form id="contact-form" @submit="checkForm">
        <sui-form-group action="">
            <sui-grid divided="vertically">
                <sui-grid-row :columns="2">
                    <sui-grid-column>
                        <div class="field">
                            <label>First Name*</label>
                            <sui-input
                                placeholder="John"
                                v-model="firstname"
                            />
                        </div>
                    </sui-grid-column>
                    <sui-grid-column>
                        <div class="field">
                            <label>Last Name*</label>
                            <sui-input
                                placeholder="Doe"
                                v-model="lastname"
                            />
                        </div>
                    </sui-grid-column>
                </sui-grid-row>

                <sui-grid-row :columns="2">
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

                <sui-grid-row :columns="2">
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
                            <label>Phone*</label>
                            <sui-input
                                placeholder="0123124244"
                                v-model="mobile"
                            />
                        </div>
                    </sui-grid-column>
                </sui-grid-row>

                <sui-grid-row :columns="1">
                    <sui-grid-column>
                        <div class="field">
                            <label>Image-Url</label>
                            <sui-input
                                placeholder="https://example.com/image.png"
                                v-model="image"
                            />
                        </div>
                    </sui-grid-column>
                </sui-grid-row>

                <sui-grid-row :columns="3">
                    <sui-grid-column>
                        <sui-button color="green" type="button" @click="createContact">
                            <sui-icon name="check" />
                            Submit
                        </sui-button>
                    </sui-grid-column>
                    <sui-grid-column>
                        <sui-button color="red" type="button" @click="cancelContact">
                            <sui-icon name="cancel" />
                            Cancel
                        </sui-button>
                    </sui-grid-column>
                    <sui-grid-column>
                        *field is required
                    </sui-grid-column>
                </sui-grid-row>
            </sui-grid>
        </sui-form-group>
    </sui-form>
    <sui-header as="h4" textAlign="center" color="red">{{this.error}}</sui-header>
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
                mobile: '',
                image: '',
                error: ''
            }
        },
        
        methods: {
            
            async createContact() {
                
                if(this.firstname === '' || this.lastname === '' || this.mobile === ''){
                    this.error = 'pls fill required fields!'
                    return false;
                }

                try {
                    const data = {
                        "firstname" : this.firstname,
                        "lastname" : this.lastname,
                        "middlename" : this.middlename,
                        "gender" : this.gender,
                        "email" : this.email,
                        "mobile" : this.mobile,
                        "image": this.image
                    }

                    let response = await fetch('https://backend-justin-dhbw.onrender.com/contacts/', {
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

            cancelContact() {
                this.$emit('showEvent')
            }

        }
    }
</script>