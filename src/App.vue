<template>
  <v-app>
    <div class="rickandmorty">
      <v-btn class="botao-buscar" @click="novopersonagem">Buscar Personagem</v-btn>
      <div class="personagem" v-if="personagem">
        <h3> Name: {{ personagem.name }} </h3>
        <h3> Status: {{ personagem.status }}</h3>
        <img :src="personagem.image" class="personagem-imagem"/>
      </div>
    </div>
    <!-- 
    Tarefa:
    - Conseguir se conectar/consumir API rick and morty (https://rickandmortyapi.com/api/character)
    - Quando clicar no botao, exibir o nome, status, imagem Do Rick Sanchez.
    - Estrutura do layoult 
      Botão de buscar novo personagem
      
      Rick Sanches - Alive
      Foto dele embaixo 
   -->
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  data: () => ({
    personagem: null,
    url: "https://rickandmortyapi.com/api/character",
  }),

  created() {
    this.novopersonagem();
  },

  methods: {
    async novopersonagem() {
      try {
        const response = await axios.get(this.url);
        const personagemAleatorio = response.data.results[Math.floor(Math.random() * response.data.results.length)];
        this.personagem = personagemAleatorio;
      }
      catch (error) {
        console.error("Erro ao buscar personagem:", error);
      }
      
    },
  }
};

</script>


<style>
  .rickandmorty {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #6ddc94;
  text-align: center;
}

.botao-buscar {
  margin-bottom: 20px;
  background-color: #78abf7 !important;
  font-size: 14px;
  padding: 10px 20px;
  border-radius: 8px;
}

.personagem-imagem {
  margin-top: 15px;
  border-radius: 10px;
  max-width: 500px;
}

</style>