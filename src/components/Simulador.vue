<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex xs12>
        <v-img
          :src="require('../assets/logo.png')"
          class="my-3 mx-auto"
          contain
          height="200"
          width="150"
        ></v-img>
      </v-flex>

      <v-flex mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          Bem Vindo ao Future Encrypt
        </h1>
        <p class="subheading font-weight-regular">
          Sistema Desenvolvido para criptografia de senhas onde mostra o resultado em Hexadecial, porem antes é feito a conversão em Binário
          <br>Por Favor, escolha uma das opções e teste o sistema.
        </p>
        <v-radio-group v-model="switch1" row>
          <v-radio label="Criptografar" :value="true"></v-radio>
          <v-radio label="Descriptografar" :value="false"></v-radio>
        </v-radio-group>
        <v-text-field :label="switch1 ? 'Senha' : 'Chave'" v-model="senha" filled/>
        <v-btn class="mx-2" color="primary" @click="submit()">{{ switch1 ? 'Criptografar'  : 'Descriptografar'}}</v-btn>
        <v-btn class="mx-2" color="warning" outlined @click="limpar()">Limpar</v-btn>
        <v-alert
          v-show="resultado!== ''"
          icon="mdi-shield-lock-outline"
          prominent
          text
          type="info"
          class="my-5"
        >
        <v-row align="center">
            <v-col class="grow">
               Sua Chave é: <br>
              {{ resultado }}</v-col>
          </v-row>
       
        </v-alert>
      </v-flex>

    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    senha: '',
    resultado: '',
    switch1: true
  }),
  methods: {
    submit(){
      const arrayBin = [];
      const arrayHex = [];
      if(this.switch1){
        const array = this.senha.split("");
        array.forEach(letra => {
          arrayBin.push(this.convertBin(letra))
        })
        arrayBin.forEach(binario =>{
          arrayHex.push(this.convertHex(binario))
        })
        this.resultado = arrayHex.reverse().join('-')
      }else{
         const array = this.senha.split("-");
        array.reverse().forEach(hex =>{
          arrayHex.push(this.convertHex(hex))
        })
        arrayHex.forEach(bin =>{
          arrayBin.push(this.convertBin(bin))
        })
          this.resultado = arrayBin.join('')
      }
    },
    convertBin(letra){
      return this.switch1 ? letra.charCodeAt(0).toString(2) : String.fromCharCode(parseInt(letra,2))
    },
    convertHex(binario){
      return this.switch1 ? parseInt(binario).toString(16) : parseInt(binario,16).toString()
    },
    limpar(){
      this.resultado = '';
      this.senha = '';
    }
  }
};
</script>
