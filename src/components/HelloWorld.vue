<template>
   
    <div id="main">
      <div id="poketable">
      <h2>Pokédex Shiny de Kanto</h2>
      <input class="recherche" type="number" v-on:change="recherchepk" />
      <table> 
      <thead>
        <tr>
          <th>
            {{ this.namepk }}
          </th>
          <th>
            {{ this.idpk }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr> 
          <td> 
            <img id="source" />
          </td>
        </tr>
        <tr> 
        <th>
          Type
        </th>
          <td> 
            <li v-for="value in this.typepk" v-bind:key="value">
              {{ value.type.name }}
            </li>
          </td>
        </tr>
       </tbody>
      </table>
      </div>

      <!-- <p>{{ this.namepk }} {{ this.idpk }}</p>
      <ul>
        <li v-for="value in this.typepk" v-bind:key="value">
          {{ value.type.name }}
        </li>
      </ul>
      <img id="source" /> -->
    </div>
</template> 

<script>
import axios from "axios";
export default {
  name: "hello",
  data() {
    return {
      namepk: null,
      imagepk: null,
      typepk: null,
      idpk: null
    };
  },
  methods: {
   

    recherchepk: function(event) {
      var url = "https://pokeapi.co/api/v2/pokemon/" + event.target.value;
      console.log(url);
      axios.get(url).then(response => {
        this.namepk = response.data.name;
        this.idpk = response.data.id;
        this.imagepk = response.data.sprites.front_shiny;
        this.typepk = response.data.types;
        document.getElementById("source").src = this.imagepk;
      });
    }
  },
  mounted() {}
};
</script>

<style scoped>
#poketable {
    width:100%;
    height:100%;
    font-weight: bold;
  }

table {
    width: 50%;
    margin: 0 auto; 
    margin: 1em auto 1em auto;
    border: 1px solid #aaa;
    padding: 3px;
    background-color: #e4f5dc
  }

th {
  background-color:  #7bce52;
  padding: 10px;
}

ul {
  list-style: none;
}

li {
  padding: 5px;
}
img {
    width: 35%;
    height: auto;}

#main {
  text-align: center;
}
.recherche {
  width: 50%;
  padding: 10px;
}
td {
  text-align: center;
}
</style>
