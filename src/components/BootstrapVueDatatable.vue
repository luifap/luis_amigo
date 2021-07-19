<template>
  <div>
    <div class="text-center">
      <b-card
        overlay
        img-src="https://picsum.photos/900/250/?image=3"
        img-alt="Card Image"
        text-variant="white" 

      >
      <br><br><br><br>
      <b-card-text class="title">
          Lorem ipsum dolor 
        </b-card-text>
      <b-card-text class="sub-title">
          Lorem ipsum dolor 
        </b-card-text>
        <b-card-text >
          Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quas numquam velit totam inventore molestiae error aliquam facere neque dolor ex voluptatibus non.
        </b-card-text>
      </b-card>
    </div>
    <br><br>
    <h1 class="title text-center">
          <span class="has-text-success text-center" > Listado Gamers</span>
      </h1> 
    <b-row>
      <b-col md = "3">
        <b-form-input 
        v-model= "filter" 
        type = "Search" 
        placeholder= "Buscar">
        </b-form-input>
      </b-col>      
    </b-row><br>
    <b-table striped hover :items= "items" :fields= "fields"  :filter= "filter" ></b-table>

  </div>
</template>

<script>
  export default {
    data() {
      return {
        filter: "",
        fields: [
          {
            key: 'Apellido',
            sortable: true
          },
          {
            key: 'Nombre',
            sortable: false
          },
          {
            key: 'Edad',
            sortable: true,
          },
          
        ],
        items: [
          { isActive: true, Edad: 40, Apellido: 'Juan', Nombre: 'Parra' },
          { isActive: false, Edad: 21, Apellido: 'Pepe', Nombre: 'Arboleda' },
          { isActive: false, Edad: 33, Apellido: 'Gabriela', Nombre: 'Restrepo' },
          { isActive: true, Edad: 38, Apellido: 'Jami', Nombre: 'Cano' }
        ]
      }
    }
  }
</script>