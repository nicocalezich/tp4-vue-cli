<template>

  <div class="jumbotron">
    <button @click="getDataXML()" type="button" class="btn btn-primary my-3 me-3 ms-3">XMLHttpRequest</button>
    <button @click="getDataFetch()" type="button" class="btn btn-secondary my-3 me-3">fetch</button>
    <button @click="getDataAxios()" type="button" class="btn btn-success my-3 me-3">axios</button>
  <div class="table-responsive">
  <table class="table">
      <thead>
        <tr class="table-primary">
          <th class="table-primary" scope="col">Nombre</th>
          <th class="table-primary" scope="col">Email</th>
          <th class="table-primary" scope="col">Telefono</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(object,index) in data" :key="index" class="table-darprimaryk">
          <td class="table-primary">{{object.nombre}}</td>
          <td class="table-primary">{{object.email}}</td>
          <td class="table-primary">{{object.nombre}}</td>
        </tr>
      </tbody>
  </table>
  </div>
  </div>

</template>

<script lang="js">

  export default  {
    name: 'src-components-data',
    props: [],
    mounted () {

    },
    data () {
      return {
        url: 'https://60aa960a66f1d00017773022.mockapi.io/Usuarios',
        data: []
      }
    },
    methods: {
      getDataXML(){
        let xhr = new XMLHttpRequest
        xhr.open('get',this.url)
        xhr.addEventListener('load',() =>{
          if(xhr.status == 200){
            this.data = JSON.parse(xhr.response)
          }
          else{
            console.error(`Error en get -> ${xhr.status}`)
          }
        })
        xhr.send()
      },

      getDataFetch(){
        fetch(this.url).then(data => data.json()).then(response =>{
         this.data = response
        })
        .catch(error => console.error(error))
      },

      getDataAxios(){
        this.axios(this.url)
        .then(response =>{
          this.data = response.data
        })
      }

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron{
    background-color: rgb(140, 168, 221);
  }
</style>
