<template>
  <div>
    <v-app-bar color="primary darken-3" clipped dark app>
      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
      <div class="d-flex align-center">
        <v-img
          alt="SGOT"
          class="shrink mr-2"
          contain
          src="../assets/truck.png"
          transition="scale-transition"
          width="35"
        />
        <span class="shrink mt-1 hidden-sm-and-down">SGOT</span>
      </div>

      <v-spacer></v-spacer>

      <v-btn href="https://github.com/douglasbaltazar" target="_blank" text>
        <span class="mr-2">GitHub/dougBaltazar</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group
          v-model="group"
          active-class="darken-3--text text--accent-4"
        >
          <v-list-item to="/">
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>
          <v-list-item to="/pedidos">
            <v-list-item-icon>
              <v-icon>mdi-archive</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Cadastrar novo Pedido</v-list-item-title>
          </v-list-item>
          <v-list-item to="/ordens">
            <v-list-item-icon>
              <v-icon>mdi-archive-arrow-up</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Pedidos com Valor > 500</v-list-item-title>
          </v-list-item>
          <v-list-item to="/about">
            <v-list-item-icon>
              <v-icon>mdi-account</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Sobre</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    group: null,
  }),
};
</script>

<style>
</style>