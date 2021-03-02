<template>
    <v-container>
        <div>
            <h1>LOGIN</h1>
            <v-form>
                <v-text-field v-model="loginForm.name" label="name" type="text" required></v-text-field>
                <v-text-field v-model="loginForm.password" label="password" type="password" required></v-text-field>
                <v-btn type="submit" @click="login">LOGIN</v-btn>
            </v-form>
        </div>
    </v-container>

</template>

<script>
import axios from "axios";

export default {
name: "Login",
    data: () => ({
        loginForm: {
            name: '',
            password: '',
        },
        loggedUser: '',
    }),
    methods: {
        login: async function () {
            // eslint-disable-next-line no-unused-vars
            let response = await axios.get('http://trakomlat/api/user', this.loginForm);
            return response => this.loggedUser = response.data;
        }
        }
    }
</script>

<style scoped>

</style>