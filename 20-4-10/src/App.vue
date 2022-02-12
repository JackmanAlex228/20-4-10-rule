<template>
  <v-app>
    <v-main>
      <Form/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import Form from './components/Form';

export default {
  name: 'App',

  components: {
    Form
  },

  data: () => ({
    //
  }),
};
</script>
