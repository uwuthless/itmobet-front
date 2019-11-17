<template>
    <div id="find_todo">
        <form @submit.prevent="doLogin">
            <input type="text" v-model="login" name="Login" placeholder="Login">
            <input type="text" v-model="pass" name="Pass" placeholder="Password">
            <input type="submit" value="Submit" class="btn">
            <div>Your balance now is: {{balance}}</div>
        </form>
    </div>
</template>

<script>
    import axios from 'axios';
    import Vue from 'vue';
    import VueCookies from 'vue-cookies';
    Vue.use(VueCookies)
    // set default config
    VueCookies.config('7d')



    export default {
        name: "LoginPass",
        data(){
            return{
                login: '',
                pass: ''
            }
        },
        props: ["balance"],
        methods: {
            async doLogin(){
                window.console.log("starting")
                const userData = (await axios.get(`http://localhost:3000/user?name=${this.login}&pass=${this.pass}`)).data
                window.console.log(userData)
                if(userData._id == undefined){
                    return;
                }
                VueCookies.set('_id',userData._id);
                this.balance = userData.balance;
                window.console.log("done. here are cookies: "+ VueCookies.get('_id'))

            }
        }
    }
</script>

<style scoped>

</style>