<template>
  <v-container>
    <h1>Consulta de Categorias</h1>
    <hr>
    <v-container>
      <v-row>
        <v-col>
          <v-btn
            outlined
            @click="getCategorias"
          >
            Pesquisar
          </v-btn>
        </v-col>
        <v-col>
          <v-btn
            outlined
            to="/categorias/cadastro"
          >
            Cadastrar
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
    <v-container>
      <v-data-table
        :headers="headers"
        :items="categorias"
        :items-per-page="10"
        class="elevation-1"
      ></v-data-table>
    </v-container>
  </v-container>
</template>

<script>
export default {
  name: 'ConsultaCategoriasPage',

  data () {
    return {
      headers: [
        {
          text: 'Código', //nome da coluna
          align: 'center', //alinhamento -center, end, start
          sortable: false, //se permite ordenação dos dados por essa coluna
          value: 'id', //é o dado que essa coluna vai receber
        },
        {
          text: 'Nome',
          align: 'center',
          sortable: false,
          value: 'nome',
        }
      ],
      categorias: []
    }
  },

  created () { //executado toda vez que a pagina é carregada
    this.getCategorias()
  },

  methods: {
    async getCategorias () {
      this.categorias = await this.$axios.$get('http://localhost:3333/categorias');
    }
  }

}
</script>