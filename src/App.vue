<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>FutureCrypt</span>
        <span class="font-weight-light"></span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        text
        href="https://futureagencia.herokuapp.com/"
        target="_blank"
      >
        <span class="mr-2">Future Agência</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <Simulador/>
    </v-content>
  </v-app>
</template>

<script>
import Simulador from './components/Simulador';

export default {
  name: 'App',
  components: {
    Simulador,
  },
  data: () => ({
    //
  }),
};
</script>
