<template>
  <div>
      <login></login>
      <create></create>
    <display></display>
  </div>
</template>

<script>
import Display from "@/components/Display";
import Create from "@/components/Create";
import Login from "@/components/Login";

export default {
  name: 'App',

  components: {
    Display,Create,Login
  },

  data: () => ({
    //
  }),
};
</script>
