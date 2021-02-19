<template>
  <div>
    <p>{{ info }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      info: null
    }
  },
  mounted() {
    axios
      .get('http://trakomlat/api/music/')
      .then(response=>(this.info = response.data))
  }
}
</script>

<style scoped>

</style>
