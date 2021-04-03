<template>
  <v-card-text>
    <v-form class="px-3" ref="form">
      <v-text-field
        label="Nome Produto 1"
        counter="50"
        v-model="form.produto1"
        prepend-icon="mdi-archive"
        :rules="produtoRules"
      ></v-text-field>
      <v-text-field
        label="Valor Produto 1"
        type="number"
        v-model="form.valorp1"
        @input="calculo"
        prepend-icon="mdi-currency-brl"
        :rules="valorRules"
      ></v-text-field>
      <v-text-field
        label="Nome Produto 2"
        counter="50"
        v-model="form.produto2"
        prepend-icon="mdi-archive"
      ></v-text-field>
      <v-text-field
        label="Valor Produto 2"
        type="number"
        @input="calculo"
        v-model="form.valorp2"
        prepend-icon="mdi-currency-brl"
      ></v-text-field>
      <v-text-field
        label="Nome Produto 3"
        counter="50"
        v-model="form.produto3"
        prepend-icon="mdi-archive"
      ></v-text-field>
      <v-text-field
        label="Valor Produto 3"
        type="number"
        @input="calculo"
        v-model="form.valorp3"
        prepend-icon="mdi-currency-brl"
      ></v-text-field>
      <v-text-field
        label="Valor Total"
        disabled
        type="number"
        v-model="form.valortotal"
        prepend-icon="mdi-currency-brl"
      ></v-text-field>
      <v-btn text class="primary mx-0 mt-3  mr-2" @click="submit"
        >Adicionar Pedido</v-btn
      >
      <v-btn text class="error mx-0 mt-3" @click="clear"
        >Limpar</v-btn
      >
    </v-form>
  </v-card-text>
</template>

<script lang="ts">
import apiService from '@/services/apiService';
export default {
  name: "PedidoForm",
  data: () => ({
    form: {
      produto1: "",
      valorp1: 0,
      produto2: "",
      valorp2: 0,
      produto3: "",
      valorp3: 0,
      valortotal: 0,
    },
    produtoRules: [
      (v) => (v && v.length >= 3) || "Cadastre ao menos um produto no Pedido",
      (v) => (v && v.length < 50) || "O tamanho maximo é 50 caracteres.",
    ],
    valorRules: [(v) => !!v || "Cadastre um valor para um Produto"],
  }),
  methods: {
    submit(): void {
      if (this.$refs.form.validate()) {
        const obj = {
          product1: this.form.produto1,
          product2: this.form.produto2,
          product3: this.form.produto3,
          valueProduct1: this.form.valorp1,
          valueProduct2: this.form.valorp2,
          valueProduct3: this.form.valorp3,
          totalValue: parseInt(this.form.valorp1) + parseInt(this.form.valorp2) + parseInt(this.form.valorp3),
          sent: false
        }
        apiService.createOrder(obj)
          .then(res => {
            alert('Cadastrado com sucesso')
            this.$router.push('/')
          }).catch(() => {
            alert('Erro no cadastro')
          })
      }
    },
    clear(): void {
      this.$refs.form.reset()
    },
    calculo(): void {
      this.form.valortotal = parseInt(this.form.valorp1) + parseInt(this.form.valorp2) + parseInt(this.form.valorp3)
    }
  },
};
</script>

<style>
</style>