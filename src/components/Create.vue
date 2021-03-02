<template>
    <v-container>
        <!-- form to create account-->
        <div>
            <v-form>
                <h1>CREATE ACCOUNT</h1>
                <v-text-field v-model="createAccountForm.name" label="Name"  type="text" required></v-text-field>
                <v-text-field v-model="createAccountForm.email" label="Email"  type="email" required></v-text-field>
                <v-text-field v-model="createAccountForm.password" label="password" type="password" required></v-text-field>
                <v-btn type="submit" @click="createAccount">SUBMIT</v-btn>
            </v-form>
        </div>
    </v-container>
</template>

<script>
import axios from "axios";
export default {
name: "Create",
    data: () => ({
        createAccountForm: {
            name: '',
            email: '',
            password: '',
        }
    }),
    methods: {
    createAccount: function () {
        axios
        .post('http://trakomlat/api/user', this.createAccountForm)
            .then(function (response) {
                console.log(response)
            })
            .catch(function (error) {
                console.log(error)
            })
    }
    }
}
</script>

<style scoped>

</style>