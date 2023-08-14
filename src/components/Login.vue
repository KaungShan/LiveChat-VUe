<template>
    <form @submit.prevent="Login">
        <h1>Login</h1>
        <input type="email" v-model="email" placeholder="email">
        <input type="password" v-model="password" placeholder="password">
        <button>Log in</button>
    </form>
</template>
<script>
import { ref } from 'vue'

export default {
    setup(){
        let email=ref("")
        let password=ref("")
        let Login=()=>{
            console.log(email.value, password.value)
        }
        return{email,password,Login};
    }
}
</script>
<style>
    
</style>