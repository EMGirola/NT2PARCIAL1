<template>

<section class="src-components-form-user-form">
  <div class="jumbotron">

    <h1>Formulario de inserción</h1>
    <br/>

    <vue-form :state="formState" @submit.prevent="submitForm()">

      <validate tag="div">
        <label for="name">Nombre</label>
        <input 
          type="text" 
          id="name" 
          name="name" 
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.name"
          required
          nospaces
          :minlength="nameLengthMin"
          :maxlength="nameLengthMax"
        >
        <field-messages name="name" show="$dirty">
          <div slot="nospaces" class="alert alert-danger">No se permiten espacios</div>            
          <div slot="required" class="alert alert-danger">Campo requerido</div>            
        
          <div slot="minlength" class="alert alert-danger">
            Minimos caracteres no alcanzados, cantidad: {{ nameLengthMin }} caracteres
          </div>            
          <div v-if="formData.name.length == nameLengthMax" class="alert alert-warning">
            Maximos caracteres alcanzados, cantidad: {{ nameLengthMax }} caracteres
          </div>            
        </field-messages>

      </validate>
      <br/>
      <validate tag="div">
        <label for="lastname">Apellido</label>
        <input 
          type="text" 
          id="lastname" 
          name="lastname" 
          class="form-control"
          autocomplete="off"
          v-model.trim="formData.lastname"
          required
          nospaces
          :minlength="nameLengthMin"
          :maxlength="nameLengthMax"
        >
        <field-messages name="lastname" show="$dirty">
          <div slot="nospaces" class="alert alert-danger">No se permiten espacios</div>            
          <div slot="required" class="alert alert-danger">Campo requerido</div>            
        
          <div slot="minlength" class="alert alert-danger">
            Minimos caracteres no alcanzados, cantidad: {{ nameLengthMin }} caracteres
          </div>            
          <div v-if="formData.name.length == nameLengthMax" class="alert alert-warning">
            Maximos caracteres alcanzados, cantidad: {{ nameLengthMax }} caracteres
          </div>            
        </field-messages>

      </validate>
      <br/>

      <validate tag="div">
        <label for="nota">Nota</label>
        <input 
          type="number" 
          id="nota" 
          name="nota" 
          class="form-control"
          autocomplete="off"
          v-model.number="formData.nota"
          required
          :min="notaMinima"
          :max="notaMaxima"
        >

        <field-messages name="nota" show="$dirty">
          <div slot="required" class="alert alert-danger">Campo requerido</div>            
          <div slot="min" class="alert alert-danger">Nota minima: {{notaMinima}}</div>            
          <div slot="max" class="alert alert-danger">Nota maxima: {{notaMaxima}}</div>            
        </field-messages>

      </validate>
      <br>


      <button class="btn btn-success my-3" :disabled="formState.$invalid" type="submit">Insertar</button>

    </vue-form>


  </div>


  <TableUsers v-bind:usersToShow="this.submittedUsers" />

</section>

</template>

<script lang="js">

  import TableUsers from './TableUsers';

  export default  {
    name: 'src-components-form-user-form',
  components: {
    TableUsers
  },
  props: [],
  data () {
    return {
      submittedUsers : [],
      formData : this.getInicialData(),
      formState : {},
      nameLengthMin : 3,
      nameLengthMax : 15,
      notaMinima : 0,
      notaMaxima : 10
    }
  },
  computed: {

  },
  mounted () {

  },
  methods: {
    getInicialData() {
      return {
        name: '',
        lastname: '',
        nota: ''
      }
    },

    upFirstLetter(data) {
      return data[0].toUpperCase() + data.slice(1);
    },

    submitForm() {
      let newUser = {
        name: `${this.upFirstLetter(this.formData.name)} ${this.upFirstLetter(this.formData.lastname)}`,
        nota: this.formData.nota

      };

      
      this.submittedUsers.push(newUser);
      this.formData = this.getInicialData()
      this.formState._reset()
    }

  }
}


</script>

<style scoped lang="css">



</style>
