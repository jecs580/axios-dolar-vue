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
    @change="getDolar(fecha)"
    ></v-date-picker>
  </v-card>
  <v-card dark color="error">
    <v-card-text class="display-1 text-center">{{valor? valor:'NaN'}}</v-card-text>
  </v-card>
  </v-flex>
 
</v-layout>
</div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'Home',
    components: {
    },
    data () {
      return {
        fecha: new Date().toISOString().substr(0, 10).replace(new Date().getDate()+1,new Date().getDate()),
        minimo:'1984',
        maximo: new Date().toISOString().substr(0, 10).replace(new Date().getDate()+1,new Date().getDate()),
        valor:null
      }
      },
      methods:{
        async getDolar(dia){
          let arrayFecha= dia.split(['-']);
          arrayFecha.reverse();
          let fecha =  arrayFecha.join('-')
          try {
            let datos = await axios.get(`https://mindicador.cl/api/dolar/${fecha}`);
            if(datos.data.serie[0]!== undefined){
              this.valor = datos.data.serie[0].valor;
            }else{
              this.valor= null;
            }
          } catch (error) {
            console.log(error);
          }
        }
      },
      created(){
        this.getDolar(this.fecha);
      }
  }
</script>
