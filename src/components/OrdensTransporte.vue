<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <template>
          <v-data-table
            :headers="headers"
            :items="pedidos"
            sort-by="calories"
            class="elevation-1"
          >
            <template v-slot:top>
              <v-toolbar flat>
                <v-toolbar-title
                  >Pedidos com Valor Total acima de 500</v-toolbar-title
                >
                <v-divider class="mx-4" inset vertical></v-divider>
                <v-spacer></v-spacer>
                <v-dialog v-model="dialog" max-width="500px">
                  <v-card>
                    <v-card-title>
                      <span class="headline">{{ formTitle }}</span>
                    </v-card-title>

                    <v-card-text>
                      <v-container>
                        <v-row>
                          <v-col cols="12" sm="6" md="8">
                            <v-text-field
                              v-model="produtoItem.product1"
                              counter="50"
                              label="Produto 1"
                              :rules="produtoRules"
                              prepend-icon="mdi-archive"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="produtoItem.valueProduct1"
                              label="Valor Produto 1"
                              @input="calcular"
                              type="number"
                              :rules="valorRules"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="8">
                            <v-text-field
                              counter="50"
                              v-model="produtoItem.product2"
                              prepend-icon="mdi-archive"
                              label="Produto 2"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="produtoItem.valueProduct2"
                              label="Valor Produto 2"
                              @input="calcular"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="8">
                            <v-text-field
                              counter="50"
                              v-model="produtoItem.product3"
                              prepend-icon="mdi-archive"
                              label="Produto 3"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="4">
                            <v-text-field
                              v-model="produtoItem.valueProduct3"
                              label="Valor Produto 3"
                              @input="calcular"
                              type="number"
                            ></v-text-field>
                          </v-col>
                          <v-col cols="12" sm="6" md="12">
                            <v-text-field
                              v-model="produtoItem.totalValue"
                              label="Valor Total"
                              prepend-icon="mdi-currency-brl"
                              disabled
                              type="number"
                            ></v-text-field>
                          </v-col>
                        </v-row>
                      </v-container>
                    </v-card-text>

                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="close">
                        Sair
                      </v-btn>
                      <v-btn color="blue darken-1" text @click="save">
                        Salvar
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
                <v-dialog v-model="dialogDelete" max-width="500px">
                  <v-card>
                    <v-card-title class="headline"
                      >Are you sure you want to delete this item?</v-card-title
                    >
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn color="blue darken-1" text @click="closeDelete"
                        >Cancel</v-btn
                      >
                      <v-btn
                        color="blue darken-1"
                        text
                        @click="deleteItemConfirm"
                        >OK</v-btn
                      >
                      <v-spacer></v-spacer>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </v-toolbar>
            </template>
            <template v-slot:item.actions="{ item }">
              <v-icon small class="mr-2" @click="editItem(item)">
                mdi-pencil
              </v-icon>
              <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
            </template>
            <template v-slot:no-data>
              <v-btn color="primary" @click="pegarPedidos500">
                Tentar Novamente
              </v-btn>
            </template>
          </v-data-table>
        </template>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import apiService from "@/services/apiService";
import Vue from "vue";

export default Vue.extend({
  name: "OrdensTransporte",
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "ID",
        align: "start",
        sortable: false,
        value: "id",
      },
      { text: "Produto 1", value: "product1", sortable: false },
      { text: "Produto 2", value: "product2", sortable: false },
      { text: "Produto 3", value: "product3", sortable: false },
      { text: "Valor Total", value: "totalValue" },
      { text: "Ações", value: "actions", sortable: false },
    ],
    pedidos: [] as any,
    produtoIndex: -1,
    produtoItem: {
      id: 0,
      product1: "",
      product2: "",
      product3: "",
      valueProduct1: 0,
      valueProduct2: 0,
      valueProduct3: 0,
      totalValue: 0,
    },
    defaultProduto: {
      id: 0,
      product1: "",
      product2: "",
      product3: "",
      valueProduct1: 0,
      valueProduct2: 0,
      valueProduct3: 0,
      totalValue: 0,
    },
  }),

  computed: {
    formTitle() {
      return this.produtoIndex === -1 ? "Novo Pedido" : "Editar Pedido";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  async created() {
    this.pegarPedidos500();
  },

  methods: {
    async pegarPedidos500() {
      apiService.getOrdersAbove500().then((response) => {
        this.pedidos = response.data;
      });
    },

    editItem(item: any) {
      this.produtoItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item: any) {
      this.produtoItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.produtoItem = Object.assign({}, this.defaultItem);
      });
    },
    calcular() {
      this.produtoItem.totalValue =
        parseInt(this.produtoItem.valueProduct1) +
        parseInt(this.produtoItem.valueProduct2) +
        parseInt(this.produtoItem.valueProduct3);
    },
    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.produtoItem = Object.assign({}, this.defaultItem);
      });
    },
    save() {
      if (this.produtoIndex > -1) {
        Object.assign(this.pedidos[this.produtoIndex], this.produtoItem);
      } else {
        this.pedidos.push(this.produtoItem);
      }
      this.close();
    },
  },
});
</script>
