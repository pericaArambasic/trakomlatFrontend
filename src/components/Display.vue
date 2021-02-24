<template>

    <v-container >
        <!-- div that contains ytb link from database-->
        <div v-for="item in info" :key="item.id">
          <iframe width="560" height="315" :src="'https://www.youtube.com/embed/' + item.link"
                  frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
          <h4>{{ item.name }}</h4>
          <p>{{item.link}}</p>

          <!--form that deletes current link-->
          <v-form>
            <p>http://trakomlat/api/music/{{item.id}}</p>
              <v-btn type="submit" @click="deleteLink(item.id)">DELETE {{item.id}}</v-btn>
          </v-form>
        </div>

      <!-- form that submits new link to a database-->
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
      // eslint-disable-next-line no-unused-vars
      let proper = null;
      proper = this.form.link.split("=");
      proper = this.form.link[0];
      axios
          .post('http://trakomlat/api/music', this.form)
      .then(function (response) {
        console.log(response)
      })
      .catch(function (error) {
        console.log(error)
      })
    },

    deleteLink: function (id)
    {
      axios
      .delete('http://trakomlat/api/music/'+ id)
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