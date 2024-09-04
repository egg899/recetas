<template>
  <div class="container">
    <div class="ver">
      <div class="form" v-if="localStorageItems.length > 0">
        <h1>Ejercicio Integrador</h1>
        <h1>Bienvenido {{ localStorageItems[0].nombre }} {{ localStorageItems[0].apellido }}!!</h1>
        <div class="condicionRecetas" v-if="localStorageRecetas.length > 0">
          <p>Tenemos recetas guardadas para vos</p>
          <button @click="this.$router.push('/ver')">Ver recetas</button>
          <br /><br />
          <hr />
        </div>
        <!--condicionRecetas-->

        <form v-on:submit.prevent="guardarReceta">
          <label>Receta</label>
          <input type="text" v-model.trim="receta" placeholder="Nombre de Receta" />
          <label>Descripción</label>
          <textarea v-model="descripcion" placeholder="Descripcion de la receta..."></textarea>

          <button type="submit" value="Guardar">Guardar</button>
        </form>
        <!--form-->
      </div>
    </div>

    <!--Ver-->
  </div>
  <!--container-->
</template>

<script>
export default {
  name: 'HomeView',
  data() {
    return {
      localStorageItems: [], //Initialize empty array to hold user data
      localStorageRecetas: [],
      receta: '',
      descripcion: '',
      fecha: ''
    } //return
  }, //data
  mounted() {
    //retrieve user data from localStorage
    this.localStorageItems = JSON.parse(localStorage.getItem('user')) || []
    this.localStorageRecetas = JSON.parse(localStorage.getItem('recetas')) || []
    //redirect to login if no user data found
    if (this.localStorageItems.length === 0) {
      this.$router.push('/login')
    } //if this.localStorageItems.length
  }, //mounted
  methods: {
    guardarReceta() {
      this.$emit('receta-enviada', {
        receta: this.receta,
        descripcion: this.descripcion,
        fecha: new Date().getTime()
      })
      //Limpiar los campos
      this.receta = ''
      this.descripcion = ''
    } //guardarReceta
  }, //methods
  emits: ['receta-enviada']
} //export
</script>
