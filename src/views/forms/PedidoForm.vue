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
        prepend-icon="mdi-currency-brl"
        :rules="valorRules"
      ></v-text-field>
      <v-text-field
        label="Nome Produto 2"
        counter="50"
        v-model="form.produto2"
        prepend-icon="mdi-archive"
        :rules="produtoRules"
      ></v-text-field>
      <v-text-field
        label="Valor Produto 2"
        type="number"
        v-model="form.valorp2"
        prepend-icon="mdi-currency-brl"
      ></v-text-field>
      <v-text-field
        label="Nome Produto 3"
        counter="50"
        v-model="form.produto3"
        prepend-icon="mdi-archive"
        :rules="produtoRules"
      ></v-text-field>
      <v-text-field
        label="Valor Produto 3"
        type="number"
        v-model="form.valorp3"
        prepend-icon="mdi-currency-brl"
      ></v-text-field>
      <v-text-field
        label="Valor Total"
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
export default {
  name: "PedidoForm",
  data: () => ({
    form: {
      produto1: "",
      valorp1: "",
      produto2: "",
      valorp2: "",
      produto3: "",
      valorp3: "",
      valortotal: "",
    },
    produtoRules: [
      (v) => (v && v.length >= 3) || "Digite ao menos 3 caracteres",
      (v) => (v && v.length < 50) || "O tamanho maximo é 50 caracteres.",
    ],
    valorRules: [(v) => !!v || "Valor é requerido"],
  }),
  methods: {
    submit(): void {
      if (this.$refs.form.validate()) {
        console.log(this.form);
      }
    },
    clear(): void {
      this.$refs.form.reset()
    },
  },
};
</script>

<style>
</style>