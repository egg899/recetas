<template>
  <main>
    <!-- <h1 v-if="user.length > 0">Bienvenido {{ user[0].nombre }}, {{ user[0].apellido }} !!</h1> -->
    <div>
      <h1>Bienvenido a la seccion de Recetas!</h1>
      <h2>No tienes recetas guardadas todavía</h2>
      <h3>Haz Login</h3>

      <LoginView @formulario-enviado="formularioEnviadoHandler" />
    </div>
  </main>
</template>
<script>
import LoginView from '../components/login.vue'

export default {
  components: {
    LoginView
  },
  data() {
    return {
      user: []
    }
  },
  mounted() {
    //Busca la data inicial del local storage
    this.user = JSON.parse(localStorage.getItem('user')) || []
    console.log('Initial user data:', this.user.length)
    if (this.user.length > 0) {
      //alert(`Hola ${this.user[0].nombre} ${this.user[0].apellido}`)
      this.$router.push('/')
    }
  }, //mounted,
  methods: {
    formularioEnviadoHandler(datos) {
      //Aca recibimos los datos des login.vue
      console.log('Datos recibidos: ', datos)
      if (datos.nombre == '' || datos.apellido == '') {
        alert('No hay nada')
        return
      } else {
        //agarra data existente de localStorage
        let storedData = JSON.parse(localStorage.getItem('user')) || []

        storedData.push(datos)

        //Actualiza el localStorage con el nuvo array StorgeData
        localStorage.setItem('user', JSON.stringify(storedData))

        //Actualiza el array user
        this.user = storedData
        console.log('User Array', this.user)
        this.$router.push('/')
        //Update local Storage if there are local storage
        //localStorage.setItem('user', JSON.stringify(this.arr))
      }
    } //formualarioEnviadoHandler
  }
} //export default
</script>
