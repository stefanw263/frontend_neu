<template>

    <sui-form class="login">
        <sui-header as="h1" textAlign="center">Login</sui-header>

        <div class="field">
            <label>Username</label>
            <sui-input
                v-model="username"
            />
        </div>
        <div class="field">
            <label>Password</label>
            <sui-input 
                type="password"
                v-model="passwd"
            />
        </div>

        <sui-button type="button" @click="login">Login</sui-button>
        <p>{{this.error}}</p>
    </sui-form>

</template>

<script>


    import md5 from 'js-md5'

    export default {
        
        name: 'Login',
        props: ['auth'],
        data() {
            return {
                username: "",
                passwd: "",
                error: ""
            }
        },
        methods: {
            async login() {
                if(this.username != "" && this.passwd != "") {

                    const data = {
                        "username": this.username,
                        "passwd": md5(this.passwd)
                    }

                    let response = await fetch('https://backend-justin-dhbw.onrender.com/auth', {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json",
                         },
                        body: JSON.stringify(data)
                    })
                    
                    if(response.status === 200){
                        this.$emit("authenticated", true)
                        this.$router.replace({ name: "contacts" })
                    }
                    else {
                        this.error = 'wrong username or password'
                    }
                } else {
                    this.error = 'A username and password must be present'
                }
            }
        }
    }
</script>

<style>

.form,
.login {
    width: 90vw;
    max-width: 460px !important;
}

.form{
    margin: 20px auto;
}
.login {
    margin: 100px auto;
}
.column{
    margin: 0 !important;
}
</style>
  
  