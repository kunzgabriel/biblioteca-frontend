<template>
  <v-container>
    <h1>Cadastro de Livros</h1>
    <hr>
    <v-form>
      <v-container>
        <v-row>
          <v-col
            cols="2"
          >
            <v-text-field
              v-model="livro.id"
              placeholder="Código"
              label="Código"
              disabled
              outlined
            />
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-text-field
              v-model="livro.titulo"
              placeholder="Título"
              label="Título"
              outlined
            />
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-textarea
              v-model="livro.sinopse"
              placeholder="Sinopse"
              label="Sinopse"
              outlined
            />
          </v-col>
        </v-row>
        <v-row>
          <v-col
            cols="2"
          >
            <v-autocomplete
              v-model="livro.idAutor"
              :items="autores"
              outlined
              label="Autor"
              item-text="nome"
              item-value="id"
            ></v-autocomplete>
          </v-col>
          <v-col
            cols="2"
          >
            <v-autocomplete
              v-model="livro.idCategoria"
              :items="categorias"
              outlined
              label="Categoria"
              item-text="nome"
              item-value="id"
            ></v-autocomplete>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
    <v-btn
      outlined
      to="/livros"
    >
      Cancelar
    </v-btn>
    <v-btn
      outlined
      @click="cadastrar"
    >
      Cadastrar
    </v-btn>
  </v-container>
</template>

<script>
export default {
  name: 'CadastroLivrosPage',

  data () {
    return {
      livro: {
        id: null,
        titulo: null,
        sinopse: null,
        idCategoria: null,
        idAutor: null
      },
      categorias: [],
      autores: []
    }
  },

  created () {
    this.getAutores();
    this.getCategorias();
  },

  methods: {
    async cadastrar () {
      let livro = {
        titulo: this.livro.titulo,
        sinopse: this.livro.sinopse,
        idCategoria: this.livro.idCategoria,
        idAutor: this.livro.idAutor
      };
      let response = await this.$axios.$post('http://localhost:3333/livros', livro);
      console.log(response);
    },

    async getAutores () {
      this.autores = await this.$axios.$get('http://localhost:3333/autores');
    },

    async getCategorias () {
      this.categorias = await this.$axios.$get('http://localhost:3333/categorias');
    }
  }
}
</script>
