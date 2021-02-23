<template>

    <v-container >

        <div class="text-center" v-for="item in info" :key="item.id">

          <iframe width="560" height="315" :src="'https://www.youtube.com/embed/' + item.link"
                  frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
          <h4>{{ item.name }}</h4>
          <p>{{item.link}}</p>

        </div>

      <div>

        <v-form>

          <v-text-field v-model="form.name" label="Name of the song" required></v-text-field>

          <v-text-field v-model="form.link" label="Link" required></v-text-field>

          <v-btn type="submit" @click="submitLink">SUBMIT</v-btn>
        </v-form>
        <p>{{form}}</p>
      </div>

    </v-container>


</template>

<script>
import axios from "axios";

export default {
  name: "Display",
  data: () => ({
    info: null,
    form: {
      name: '',
      link: ''
    }
  }),
  mounted() {
    axios
     .get('http://trakomlat/api/music')
    .then(response => (this.info = response.data))
  },
  methods: {
    submitLink: function ()
    {
      axios
          .post('http://trakomlat/api/music', this.form)
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