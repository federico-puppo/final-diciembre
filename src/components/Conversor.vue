<template lang="html">
  <section class="src-components-conversor">
    <h1><b>Conversor a dólares</b></h1>
    <span>Ingrese monto $</span> <input type="number" v-model="monto"><br><br>
    <span>Valor del dolar en $</span> <input type="number" v-model="valorDolar">
    <label for="checkbox"> - {{actualizar == true ?"Actualizado a las":"Actualizacion"}} {{fechaActualizacion}}</label>
    <input type="checkbox" id="checkbox" v-model="actualizar">
    <br><br>
    <p>Valor convertido en USD: <b>{{ monto | toUSD(valorDolar)}}</b></p>
    <br>
  </section>
</template>

<script lang="js">
  export default  {
    name: 'src-components-conversor',
    props: [],
    filters:{
        toUSD : function(monto, valorDolar) {
        return (monto / valorDolar).toFixed(2)
      }
    },
    mounted () {
      this.refTimer = setInterval(() => {
        this.actualizarValorDolar()
        this.getFechaActualizacion()
      },2000)
    },
    destroyed(){
      clearInterval(this.refTimer)
    },
    data () {
      return {
        monto: 0,
        valorDolar: 0,
        actualizar: false,
        refTimer: null,
        fechaActualizacion: "",
        URL_API: 'https://www.dolarsi.com/api/api.php?type=valoresprincipales'
      }
    },
    methods: {
      async actualizarValorDolar(){
        if (this.actualizar){
        try {
            let respuesta = await this.axios(this.URL_API)
            this.valorDolar = parseFloat(respuesta.data[1].casa.venta)
          }
          catch(error) {
            console.error('Error AXIOS (async/await)', error)
          }
        }
      },
      getFechaActualizacion() {
        return this.actualizar == true ? this.fechaActualizacion = new Date().toLocaleString() : this.fechaActualizacion = ""
        },
    },  
    computed: {
    }
}
</script>
<style scoped lang="css">
</style>
