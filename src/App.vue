<template>
  <v-app>
    <v-app-bar app color="#ffb716a6">
      <v-toolbar-title class="headline text-uppercase">
        <span>Elogroup</span>
        <span class="font-weight-light"> Cadastro</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        text
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <a href="https://elogroup.com.br/"><span class="mr-2">Página Principal</span></a>
      </v-btn>
    </v-app-bar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data: () => ({
    //
  }),
};
</script>
