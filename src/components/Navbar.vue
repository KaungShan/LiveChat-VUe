<template>
   <nav v-if="user">
        <div>
        <p>Hi {{ user.displayName }}</p>
        <p class="email">logged in as {{ user.email }}</p> 
        </div>
    <button @click="logOut">log out</button>
   </nav>
</template>
<script>

import { ref } from 'vue';
import getUser from '../composables/getUser'
import { auth } from '@/firebase/config';
export default {
    setup(){
        let error=ref(null)
        let {user}=getUser()
        let logOut=async()=>{
            try {
                await auth.signOut()
            } catch (err) {
                error.value=err.message
            }
        }
  
        return{logOut,user}
    }
}
</script>
<style>
    nav {
        padding: 20px;
        border-bottom: 1px solid #eee;
        display: flex;

        justify-content: space-between;
        align-items: center;
    }
    nav p {
        margin: 2px auto;
        font-size: 16px;
        CoLor: #444;
    }
    nav p.email {
        font-size: 14px;
        color:#999;
    }
</style>