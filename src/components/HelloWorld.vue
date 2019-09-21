<template>
  <v-container>
    <v-card width="500" class="mx-auto mt-5">
      <v-card-title>

      </v-card-title>
      <v-card-text>
        <v-form>
          <v-text-field label="Nome" v-model="cadastro.nome" prepend-icon="mdi-account-circle" />
          <v-text-field label="Telefone" v-model="cadastro.telefone" prepend-icon="mdi-account-circle" />
          <v-select
            :items="items"
            v-model="cadastro.como_conheceu"
            prepend-icon="mdi-account-circle"
            label="Como nos conheceu"
          ></v-select>
          <v-radio-group v-model="cadastro.rede_social" label="Possui rede social" :mandatory="false">
            <v-radio label="Sim" value="1"></v-radio>
            <v-radio label="Não" value="0"></v-radio>
          </v-radio-group>
          <div v-if="cadastro.rede_social == '1'"> Quais?
            <v-checkbox
              v-model="cadastro.checkbox.Facebook"
              label="Facebook"
            ></v-checkbox>
            <v-checkbox
              v-model="cadastro.checkbox.LinkedIn"
              label="LinkedIn"
            ></v-checkbox>
            <v-checkbox
              v-model="cadastro.checkbox.Instagram"
              label="Instagram"
            ></v-checkbox>
          </div>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-btn color="info" @click="enviar">Enviar</v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
const axios = require('axios');
export default {
  data: () => ({
    items: ['Tv', 'Internet', 'Outros'],
    cadastro: {
      nome: null,
      telefone: null,
      como_conheceu: null,
      rede_social: null,
      checkbox: {
        Facebook: false,
        LinkedIn: false,
        Instagram: false,
      },
    },
  }),
  methods: {
    enviar(){
      axios.post('http://localhost:8080/', this.cadastro )
      .then(response => { console.log(response)})
    },
  }
};
</script>
