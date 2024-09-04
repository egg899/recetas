<template>
  <main>
    <HomeView @receta-enviada="recetaEnviadaHandler" />
  </main>
</template>

<script>
import HomeView from '../components/MensajeBienvenida.vue'

export default {
  components: {
    HomeView
  }, //components
  data() {
    return {
      receta: []
    } //receta
  }, //data
  methods: {
    recetaEnviadaHandler(datos) {
      //console.log('Recetas recibidas: ', datos)
      if (datos.receta == '' || datos.descripcion == '') {
        alert('No hay nada!!!')
        return
      } //if datos.receta or datos.descripcion
      else {
        let storedRecetas = JSON.parse(localStorage.getItem('recetas')) || []
        console.log('storedRecetas', storedRecetas)

        storedRecetas.push(datos)
        console.log('storedRecetas Llenos', storedRecetas)

        //Copia del objeto storedRecetas a storedRecetasCopy

        console.log('storedRecetas1', storedRecetas)
        //Actualiza el local Storage
        localStorage.setItem('recetas', JSON.stringify(storedRecetas))

        // //Actualiza el arrat receta
        this.receta.push(storedRecetas)
        // console.log('Receta Array', this.receta)
        this.$router.push('/ver')
      } //else
    } //recetaEnviadaHandler
  }
} //Export default
</script>
<!--SCRIPT-->
