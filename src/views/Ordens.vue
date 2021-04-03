<template>
  <div class="home">
    <OrdensTransporte />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import OrdensTransporte from '@/components/OrdensTransporte.vue'; // @ is an alias to /src

@Component({
  components: {
    OrdensTransporte,
  },
})
export default class Home extends Vue {}
</script>
