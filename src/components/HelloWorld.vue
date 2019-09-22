<template>
  <v-container>
    
    <v-card width="500" class="mx-auto mt-5">
      <v-card-title>

      </v-card-title>
      <v-card-text>
        <v-form>
          <v-layout row wrap class='pa-2'>
            <v-flex xs12 class='pa-2'>
              <v-text-field 
                label="Nome" 
                v-model="cadastro.nome"
                />
            </v-flex>
            <v-flex xs6 class='pa-2'>
              <v-text-field 
                @keypress="isNumber($event)"
                label="Telefone"
                v-model="cadastro.telefone"
                v-mask="'## - #########'"
              />
            </v-flex>
            <v-flex xs6 class='pa-2'>
              <v-select
                :items="items"
                v-model="cadastro.como_conheceu"
                label="Como nos conheceu"
              ></v-select>
            </v-flex>
            <v-flex xs6 class='pa-2'>
              <v-radio-group v-model="cadastro.rede_social" label="Possui rede social" :mandatory="false">
                <v-radio label="Sim" value="1" color="orange"></v-radio>
                <v-radio label="Não" value="0" color="orange"></v-radio>
              </v-radio-group>
            </v-flex>
            <v-flex xs12 class='pa-2'>
              <div v-if="cadastro.rede_social == '1'"> Quais?
                <v-checkbox
                  style="margin-top:-1px;"
                  v-model="checkbox"
                  label="Facebook"
                  value="Facebook"
                ></v-checkbox>
                <v-checkbox
                  style="margin-top:-25px;"
                  v-model="checkbox"
                  label="LinkedIn"
                  value="LinkedIn"
                ></v-checkbox>
                <v-checkbox
                  style="margin-top:-25px;"
                  v-model="checkbox"
                  label="Instagram"
                  value="Instagram"
                ></v-checkbox>
              </div>
            </v-flex>
          </v-layout>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-btn color="info" :disabled="enviou" @click="enviar">Enviar</v-btn>
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
    },
    checkbox: [],
    enviou: false,
  }),
  methods: {
    isNumber: function(evt) {
      evt = (evt) ? evt : window.event;
      var charCode = (evt.which) ? evt.which : evt.keyCode;
      if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46 && charCode !== 44) {
          evt.preventDefault();
      } else {
          return true;
      }
    },
    enviar(){
        this.enviou = true;
          if(this.cadastro.rede_social == '1'){
            this.cadastro.checkbox = this.checkbox;
          }
          axios.post('http://localhost:8080/', this.cadastro )
          .then(response => { console.log(response)})
        

    }
  }
};
</script>
