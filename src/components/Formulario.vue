<template>

  <div class="jumbotron">
    <vue-form :state="formState" @submit.prevent="enviar()">
      <validate tag="div">
        <label for="nombre" class="mt-1">Nombre</label>
        <input
          type="text"
          id="nombre"
          name="nombre"
          autocomplete="off"
          class="form-control mt-1"
          v-model.trim="formData.nombre"
          :minlength="caracterMin"
          :maxlength="caracterMax"
          required
        >
        <field-messages name="nombre" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Debe completar este campo</div>
          <div slot="minlength" class="alert alert-danger mt-1">Debe ingresar como minimo {{caracterMin}} caracteres</div>
          <div v-if="formData.nombre.length == caracterMax" class="alert alert-warning mt-1">Puede ingresar como maximo {{caracterMax}} caracteres</div>
        </field-messages>
      </validate> 

      <validate tag="div"> 
        <label for="edad" class="mt-1">Edad</label>
        <input 
          type="number" 
          id="edad" name="edad"
          autocomplete="off"
          class="form-control mt-1"
          v-model.trim="formData.edad"
          :min="edadMin"
          :max="edadMax"
          required
        >
        <field-messages name="edad" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Debe completar este campo</div>
          <div slot="min" class="alert alert-danger mt-1">La edad minima es de {{edadMin}} años</div>
          <div slot="max" class="alert alert-danger mt-1">La edad maxima es de {{edadMax}} años</div>
        </field-messages>
      </validate>  

       <validate tag="div"> 
        <label for="email" class="mt-1">Email</label>
        <input
          type="email"
          id="email" 
          name="email"
          autocomplete="off"
          class="form-control mt-1"
          v-model.trim="formData.email"
          required
        >
         <field-messages name="email" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Debe completar este campo</div>
          <div slot="email" class="alert alert-danger mt-1">Email invalido</div>
        </field-messages>
      </validate> 
      <button type="submit" :disabled="formState.$invalid" class="btn btn-success mt-3">Enviar</button>
    </vue-form>
    <br>
    <table class="table table-dark">
      <thead>
        <th>Nombre</th>
        <th>Edad</th>
        <th>Email</th>
      </thead>
      <tbody>   
        <tr>
          <td class="table-active">{{formData.nombre}}</td>
          <td class="table-active">{{formData.edad}}</td>
          <td class="table-active">{{formData.email}}</td>
        </tr>
      </tbody>
    </table>  
    
   
  </div>

</template>

<script lang="js">

  export default  {
    name: 'src-components-formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formData: this.getInicialData(),
        formState: {},
        caracterMin: 5,
        caracterMax: 15,
        edadMin: 18,
        edadMax: 120,
      }
    },
    methods: {
      getInicialData(){
        return{
          nombre: '',
          edad: '',
          email: ''
        }
      },

      enviar(){
        console.log({...this.formData})
        this.formData = this.getInicialData()
        this.formState._reset()
      }

    },
    computed: {

    }
}

</script>

<style scoped lang="css">

 .jumbotron{
   background-color: rgb(128, 110, 133);
   padding: 50px;
 }
 label{
   font-size: 21px;
   color: white;
 }
 table{
   color: black;
 }

 
</style>
