<template>
    <form @submit.prevent="SignUp">
        <h1>Sign Up</h1>
        <input type="text" v-model="displayName" placeholder="display name">
        <input type="email" v-model="email" placeholder="email">
        <input type="password" v-model="password" placeholder="password">
        <button>Sign Up</button>
    </form>
</template>
<script>
import { auth } from '@/firebase/config'
import { ref } from 'vue'

export default {
    setup(){
        let displayName=ref("")
        let email=ref("")
        let password=ref("")
        let error=ref(null)
        let SignUp=async()=>{
           try {
            let res=await auth.createUserWithEmailAndPassword(email.value, password.value)
            if(!res){
                throw new Error ("could not create account")
            }
            res.user.updateProfile({displayName: displayName.value})
           } catch (err) {
            error.value=err.message
           }
           
        }
        return{ displayName,email,password,SignUp};
    }
}
</script>
<style>
    
</style>