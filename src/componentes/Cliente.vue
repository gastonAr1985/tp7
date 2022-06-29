<template >

  <section class="src-componentes-cliente">
     <div class="jumbotron">
      <h1>Pedir datos</h1>
      
      <br>


      
      <button class="btn btn-success my-3 mr-3" @click="getAxiosAwait()">Con Await</button>
      <button class="btn btn-success my-3 mr-3" @click="getAxiosThen()">Con Then</button>
      <button class="btn btn-danger my-3 mr-3" @click="clientes=[]">Borrar </button>

      <div v-if="clientes.length" class="table-responsive" >
        <table class="table table-dark">
          <tr>
            <th>Nombre</th>
            <th>Email</th>
            <th>Edad</th>
          </tr>

          <tr v-for="(cliente, index) in clientes" :key="index">
              <td>{{cliente.nombre}}</td>
              <td>{{cliente.email}}</td>
              <td>{{cliente.edad}}</td>

          </tr>

        </table>
         <h4 class="alert alert-primary">se encontraron {{clientes.length}}</h4>
      </div>

     </div>
  </section>

</template>

<script >
 import axios from 'axios'
  export default  {
    name: 'src-componentes-cliente',
    props: [],
    mounted () {

    },
    data () {
      return {
         url:'https://62aa470c3b31438554453166.mockapi.io/users',
        clientes:[]
      }
    },
    methods: {
      
        async getAxiosAwait(){
           try{
      let {data} = await axios(this.url)
      this.clientes=data
      }catch(error){
         console.log("Error Axios", error)
      }
        

         },

          async getAxiosThen(){
             axios(this.url)
         .then(({data})=>{
         this.clientes=data
         })
         .catch(error => console.log("Error Axios", error))
      }
         
        
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-cliente {

  } .jumbotron {
    background-color: green;
    color:white;
  }
  hr{
    background-color: #bbb;
  }
</style>
