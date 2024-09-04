<template>
  <div class="container">
    <div class="ver">
      <div class="form">
        <form v-on:submit.prevent="editar(nuevoObj)">
          <label>Receta</label>
          <input type="text" v-model.trim="nuevoObj.receta" placeholder="Nombre de Receta" />
          <label>Descripción</label>
          <textarea
            v-model="nuevoObj.descripcion"
            placeholder="Descipción de la receta..."
          ></textarea>
          <button type="submit" value="Guardar">Guardar</button>
        </form>
        <!--form-->
      </div>
      <!--div form-->
    </div>
    <!--ver-->
  </div>
  <!--container-->
</template>

<script>
export default {
  name: 'EditarView',
  data: function () {
    return {
      local: [],
      nuevoObj: {
        receta: this.$route.params.receta,
        descripcion: this.$route.params.descripcion,
        fecha: this.$route.params.fecha
      } //nuevoObj
    } //return
  }, //data
  mounted: function () {
    this.ed()
  }, //mounted

  methods: {
    ed: function () {
      console.log('ed', this.$route.params.receta)
    }, //ed

    editar: function () {
      this.local = JSON.parse(localStorage.getItem('recetas'))
      console.log('editar local', this.local)

      for (var i = 0; i < this.local.length; i++) {
        if (this.local[i].fecha == this.nuevoObj.fecha) {
          console.log('Nuevo', this.nuevoObj)
          this.local.splice(i, 1)
          this.local.push(this.nuevoObj)
          console.log('local array editado', this.local)
        } //if
      } //for

      localStorage.setItem('recetas', JSON.stringify(this.local))
      this.$router.push('/ver')
    } //editar
  } //methods
} //export default
</script>
