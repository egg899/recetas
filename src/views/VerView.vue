<template>
  <main class="animate__animated animate__bounceIn animate__delay-2s animate__repeat-3">
    <div class="container">
      <button v-on:click="ascendente = !ascendente" :class="ascendente ? 'arrowB' : 'arrowA'">
        <span v-if="ascendente">Ordenar de Z - A </span>
        <span v-else> Ordenar de A - Z </span>
      </button>
      <div class="ver">
        <!-- {{ items }} -->
        <h1 v-if="user.length > 0">
          Datos guardados de {{ user[0].nombre }} {{ user[0].apellido }}
        </h1>

        <transition-group
          tag="div"
          enter-active-class="animate__animated  animate__bounceIn"
          leave-active-class="animate__animated animate__bounceOut"
        >
          <div class="hide">
            <div
              :class="
                ascendente
                  ? 'lista animate__animated animate__bounceInUp'
                  : 'lista animate__animated animate__bounceInDown'
              "
              v-for="item in items"
              :key="item.fecha"
            >
              <ul class="normal">
                <li>
                  <h2>{{ item.receta }}</h2>
                </li>
                <li><span>Descripción: </span> {{ item.descripcion }}</li>
              </ul>

              <div class="center">
                <router-link
                  :to="'/editar/' + item.receta + '/' + item.descripcion + '/' + item.fecha"
                  class="editar"
                  >Editar</router-link
                >

                <button @click="borrar(item)" class="borrar">Borrar</button>
              </div>
              <!--div center-->
            </div>
            <!--Lista-->
          </div>
        </transition-group>
      </div>
      <p>{{ sin_datos }}</p>
      <button v-show="local.length === 0" @click="this.$router.push('/')">Volver</button>
      <button v-show="local.length > 0" @click="this.$router.push('/')">Adherir más recetas</button>

      <!--ver-->
    </div>
    <!--container-->
  </main>
</template>
<script>
export default {
  name: 'VerView',
  data: function () {
    return {
      user: [],
      local: [],
      sin_datos: '',
      ascendente: true
    } //return
  }, //data

  mounted: function () {
    console.log('se monto')
    this.ver_local()
    this.ver_user()
  }, //mounted
  computed: {
    items() {
      let items = this.local
      let ordenar = items.sort((a, b) => {
        return a.receta < b.receta ? -1 : 1 //nombre de A a Z
      })

      if (!this.ascendente) {
        ordenar.reverse()
      }
      return ordenar
    } //items
  }, //computed
  methods: {
    ver_param(item) {
      console.log(item.titulo)
    }, //ver_param
    ver_local: function () {
      if (localStorage.recetas) {
        this.local = JSON.parse(localStorage.getItem('recetas'))
      } //if localStorage.recetas
      if (this.local.length === 0) {
        this.sin_datos = 'Es hora de cargar datos!!!'

        console.log(this.sin_datos)
      } // this.local.length === 0
    }, //ver_local
    ver_user: function () {
      if (localStorage.user) {
        this.user = JSON.parse(localStorage.getItem('user'))
      }
    }, //ver_user
    borrar: function (item) {
      this.local = JSON.parse(localStorage.getItem('recetas'))

      for (var i = 0; i < this.local.length; i++) {
        if (this.local[i].fecha === item.fecha) {
          let rta = confirm('¿Seguro qué querés borrar esta receta?')
          if (rta == true) {
            this.local.splice(i, 1)
          } //if rta
        } //if this.local[i].fecha
      } //for

      localStorage.setItem('recetas', JSON.stringify(this.local))
      this.ver_local()
    } //borrar
  } //methods
} //export
</script>
