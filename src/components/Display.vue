<template>

    <v-container>

        <div >
            <p>{{ info }}</p>
            <!-- form that submits new link to a database-->
            <div>
                <v-form>
                    <v-text-field v-model="form.name" label="Name of the song" required></v-text-field>
                    <v-text-field v-model="form.link" label="Link" required></v-text-field>
                    <v-btn type="submit" @click="submitLink">SUBMIT</v-btn>
                </v-form>
                <p>{{ form }}</p>
            </div>

            <!-- div that contains ytb link from database-->
            <div v-for="item in info" :key="item.id">
                <iframe width="560" height="315" :src="'https://www.youtube.com/embed/' + item.link"
                        frameborder="0"
                        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                        allowfullscreen></iframe>
                <h4> NAME- {{ item.name }}</h4>
                <p> LINK- {{ item.link }}</p>
                <p>user id - {{ item.user_id }}</p>

                <!--form that deletes current link-->
                <v-form>
                    <p>http://trakomlat/api/music/{{ item.id }}</p>
                    <v-btn type="submit" @click="deleteLink(item.id)">DELETE {{ item.id }}</v-btn>
                </v-form>
                <br>
            </div>

        </div>

    </v-container>


</template>

<script>
import axios from "axios";

export default {
    name: "Display",
    data: () => ({
        info: null,
        users: null,
        form: {
            name: '',
            link: ''
        },
    }),
    mounted() {
        axios
            .get('http://trakomlat/api/music')
            .then(response => (this.info = response.data))

        },
    methods: {
        submitLink: async function() {
            // eslint-disable-next-line no-unused-vars
            let firstStep = [];
            // eslint-disable-next-line no-unused-vars
            let secondStep = [];
            // eslint-disable-next-line no-unused-vars
            let thirdStep = [];

            firstStep = this.form.link.split("=");
            secondStep = firstStep[1];
            thirdStep = secondStep.split("&");
            this.form.link = thirdStep[0];

            // eslint-disable-next-line no-unused-vars
            let response = await axios.post('http://trakomlat/api/music', this.form);
            return response;

            // axios
            //     .post('http://trakomlat/api/music', this.form)
            //     .then(function (response) {
            //         console.log(response)
            //     })
            //     .catch(function (error) {
            //         console.log(error)
            //     })
        },

        deleteLink: function (selectedLink) {
            axios
                .delete('http://trakomlat/api/music/' + selectedLink)
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