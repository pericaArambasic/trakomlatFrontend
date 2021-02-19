<template>

  <div>

    <v-container>

      <template>

        <v-card
            class="mx-auto my-12"
            width="560"
            height="315"
        >
          <template slot="progress">
          </template>

          <iframe width="560" height="315" src="https://www.youtube.com/watch?v=8dhSq9mD6TI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


          <v-card-title>Cafe Badilico</v-card-title>


          <v-divider class="mx-4"></v-divider>

          <v-card-text>
            <v-chip-group
                v-model="selection"
                active-class="deep-purple accent-4 white--text"
                column
            >
              <v-chip>9:00PM</v-chip>
            </v-chip-group>
          </v-card-text>

        </v-card>
      </template>

    </v-container>

  </div>

</template>

<script>
import axios from "axios";

export default {
  name: "Display",
  data: () => ({
    info: null
  }),
  mounted() {
    axios
     .get('http://trakomlat/api/music')
    .then(response => (this.info = response.data))
  }
}
</script>

<style scoped>

</style>