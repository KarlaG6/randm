<template>
  <v-container>
    <v-layout wrap text-center>
      <v-flex >
        <h1>Rick and Morty</h1>
        <v-spacer></v-spacer> 
        <h3>Personajes</h3>
        <v-spacer></v-spacer> 
          <v-btn v-on:click="fetch" dark>Consultar</v-btn>
          <v-spacer></v-spacer> 
      </v-flex>
      </v-layout>
      <v-layout wrap>
      <v-flex v-for="character of characters" :key="character.id" xs3>
        <v-card dark @click="seemore(character.id)"  v-bind:style="styleObject">
          <v-img  :src="character.image" class="white--text" height="200px"  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)">
            <div class="overline" style="padding-left:5px; ">{{character.status}}</div>
            <v-card-title  class="fill-height align-end"  v-text="character.name"></v-card-title>
          </v-img>
        </v-card>
      </v-flex>
    </v-layout>   
  </v-container>
</template>

<script>
import axios from 'axios'

export default {
  data: function() {
    return {
      characters: [],
      styleObject: {
        color: 'red',
        fontSize: '13px'
      }
    }
  },
  methods: {
    fetch (){
      let result = axios.get('https://rickandmortyapi.com/api/character')
      .then((res)=>{
        this.characters = res.data.results;
        console.log(res.data)
      })
      .catch( (err) => console.log (err))
    },
    seemore (id){
    this.$router.push('/char')
    .$emit("showModal", id)
    },
    showModal (id){
      this.fetchOne(id)
    },
    async fetchOne (id){
      let result = await axios.get(`https://rickandmortyapi.com/api/character/${id}/`);
      this.currentCharacter = result.data;
      this.modal = true;

      console.log(this.currentCharacter, "personaje")
    }
  }
};
</script>
<style>
.flex{
  padding: 2%
}
* {
  padding: 4px;
}
h1,h3{
  color:white
}
.v-image__image.v-image__image--cover {
    border-radius: 5%;
}
.v-content__wrap {
  background-color: black
}
.v-application .align-end {
  padding-bottom: 12% !important
}
</style>
