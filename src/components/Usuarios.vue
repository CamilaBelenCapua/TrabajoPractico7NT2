<template>
  <section class="src-componentes-usuarios">
    <div class="jumbotron">
      <h2 class="usuarios">Usuarios</h2>
      <hr>
      <hr>
      <br>
      <button style="margin-left: 10px" class="btn btn-info ml-3" @click="getUsuariosAxios()">GET AXIOS</button>
      <button style="margin-left: 10px" class="btn btn-danger mr-3" @click="usuarios=[]">CLEAR</button>

        <span v-if="usuarios.length">
            <div class="media alert alert-info" v-for="(usuario,index) in usuarios" :key="index">
                <div class="media-body ml-4">
                    <h4 class="mt-0">
                        <u>Usuario {{ index + 1 }} - ID: {{ usuario.id }}</u>
                    </h4>
                    <br>
                    <p>Nombre Completo: <b>{{ usuario.nombre }}</b></p>
                    <p>Edad: <i>{{ usuario.edad }}</i></p>
                    <p>Email: {{ usuario.email }}</p>

                    <button style="margin-left: 10px" class="btn btn-danger mt-3" @click="deleteUsuario(usuario.id)">DELETE</button>
                </div>
            </div>
        </span>
        <span v-else class="alert alert-warning">
                    No hay usuarios que mostrar
        </span>
    </div>
  </section>
</template>

<script>
  export default  {
    name: 'src-componentes-api-rest-ful',
    props: [],
    mounted () {
    },
    data () {
      return {
        url: 'https://62ace499402135c7acba66cc.mockapi.io/usuarios',
        usuarios: []
      }
    },
    methods: {
  
      async getUsuariosAxios() {
       try {
          let { data } = await this.axios(this.url)
          console.log(data)
          this.usuarios = data
        }
        catch(error) {
          console.error('Error Axios', error)
        } 
      },
      async deleteUsuario(id) {
        console.log('deleteUsuario', id)
        try {
          let { data: usuario } = await this.axios.delete(this.url+'/'+id)
          console.log('AXIOS DELETE usuario', usuario)
          let index = this.usuarios.findIndex(user => user.id == usuario.id)
          if(index == -1) throw new Error('usuario no encontrado')
          this.usuarios.splice(index, 1)
        }
        catch(error) {
          console.error('Error en deleteUsuario()', error.message)
        }
      },            
    },
    computed: {
    }
}
</script>

<style scoped lang="css">
  .src-componentes-api-rest-ful {
  }
  .jumbotron {
   
  }
  .usuarios{
    text-align: center;
    color:rgb(5, 94, 97);
}
</style>