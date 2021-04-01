<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/truck.png')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Bem-Vindo ao SGOT
        </h1>

        <p class="subheading font-weight-regular">
          Foi um projeto que foi usado como processo seletivo,
          <br>e agora estou refazendo para melhor entender.
          <a
            href="https://github.com/douglasbaltazar"
            target="_blank"
          >GitHub Doug</a>
        </p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    name: 'HelloWorld',

    data: () => ({
    }),
  })
</script>
