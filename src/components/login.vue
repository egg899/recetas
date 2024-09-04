<template>
  <div class="container">
    <div class="form">
      <form @submit.prevent="enviarFormulario">
        <label for="nombre">Nombre</label>
        <input type="text" id="nombre" v-model="form_data.nombre" />
        <label for="Apellido">Apellido</label>
        <input type="text" id="apellido" v-model="form_data.apellido" />
        <button type="submit">Ingresar</button>
      </form>
      <!--<form>-->
    </div>
    <!--div class form-->
  </div>
  <!--container-->
</template>
<!--template-->

<script>
export default {
  name: 'LoginView',
  data: function () {
    return {
      form_data: {
        nombre: '',
        apellido: ''
      }, //form_data
      arr: []
    } //return
  },
  methods: {
    enviarFormulario() {
      this.$emit('formulario-enviado', {
        nombre: this.form_data.nombre.trim(),
        apellido: this.form_data.apellido.trim()
      })
      //Limpiar los campos del formulario
      this.form_data.nombre = ''
      this.form_data.apellido = ''
    } //enviarFormulario
  }, //methods
  emits: ['formulario-enviado']
}
</script>
