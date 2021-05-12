<template>
<div>
<v-layout :wrap="true">  <!-- ROW -->
  <v-flex xs12> <!-- COLUMN -->
  <v-card>
    <v-date-picker v-model="fecha"
    full-width
    locale="es-bo"
    :min="minimo"
    :max="maximo"
    ></v-date-picker>
  </v-card>
  <v-card dark color="error">
    <v-card-text class="display-1 text-center">6.98 - {{fecha}}</v-card-text>
  </v-card>
  </v-flex>
 
</v-layout>
</div>
</template>

<script>

  export default {
    name: 'Home',
    components: {
    },
    data () {
      return {
        fecha: '',
        minimo:'1984',
        maximo: new Date().toISOString().substr(0, 10).replace(new Date().getDate()+1,new Date().getDate())
      }
      }
  }
</script>
