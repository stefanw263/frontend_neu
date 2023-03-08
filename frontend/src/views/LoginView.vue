<template>

    <sui-form class="form">
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
                passwd: ""
            }
        },
        methods: {
            async login() {
                if(this.username != "" && this.passwd != "") {

                    const data = {
                        "username": this.username,
                        "passwd": md5(this.passwd)
                    }

                    let response = await fetch('http://127.0.0.1:3000/auth', {
                        method: "POST",
                        headers: {
                            "Content-Type": "application/json",
                         },
                        body: JSON.stringify(data)
                    })
                    
                    if(response.status === 200){
                        this.$emit("authenticated", true)
                        this.$router.replace({ name: "home" })
                    }
                    else {
                        console.log('wrong username or password')
                    }
                } else {
                    console.log("A username and password must be present")
                }
            }
        }
    }
</script>

<style>
.form {
    width: 360px;
    margin: 100px auto;
}
</style>
  
  