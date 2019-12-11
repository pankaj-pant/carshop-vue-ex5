<template>
  <v-container>
    <v-data-table
      :headers="headers"
      :items="cars"
      class="elevation-1"
    >
      <template slot="items" slot-scope="props">
        <td class="text-xs-left">{{ props.item.brand }}</td>
        <td class="text-xs-left">{{ props.item.model }}</td>
        <td class="text-xs-left">{{ props.item.year }}</td>
        <td class="text-xs-left">{{ props.item.color }}</td>
        <td class="text-xs-left">{{ props.item.price }}</td>        
        <td class="text-xs-left">{{ props.item.fuel }}</td>  
      </template>

      <template v-slot:item.action="{ item }">
      <v-icon
        small
        @click="deleteItem(props.item._links.car.href)"
      >
        delete
      </v-icon>
    </template>
    </v-data-table>
  </v-container>
</template>

<script>
  import axios from 'axios';
  
  export default {
    data () {
      return {
        cars: [],
        headers: [
          {text: 'Brand', align: 'left', value: 'brand'},
          { text: 'Model', align: 'left', value: 'model' },
          { text: 'Year', align: 'left', value: 'year' },
          { text: 'Color', align: 'left', value: 'color' },
          { text: 'Price', align: 'left', value: 'price' },
          { text: 'Fuel', align: 'left', value: 'fuel' },
          { text: 'Actions', value: 'action', sortable: false }
        ]
      }
    },
    methods: {
        deleteItem(car) {
            axios.delete(car)
            .then(this.getCars())
            
        },
        getCars(){
            axios.get('https://carstockrest.herokuapp.com/cars')
            .then(response => (this.cars = response.data._embedded.cars))
        }
    },
    mounted() {
        this.getCars()
    }
  }
</script>

<style>
</style>