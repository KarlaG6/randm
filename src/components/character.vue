<template>
  <v-container>
    <v-layout wrap text-center>
      <v-flex >
        <h1>Rick and Morty</h1>
        <v-spacer></v-spacer> 
        <h3>Personajes</h3>
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
    <div class="text-center">
      <v-pagination  v-model="pageSelect" :length="9" :total-visible="7" ></v-pagination>
    </div> 
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  props: ['id'],
  data: function() {
    return {
      characters: [],
      styleObject: {
        color: 'red',
        fontSize: '13px'
      },
      pageSelect:1 ,
    }
  },
  methods: {
    fetch (pageSelect){
      let result = axios.get(`https://rickandmortyapi.com/api/character/?page=${this.pageSelect}`)
      .then((res)=>{
        this.characters = res.data.results; //aquí lo que se trae de la API es almacenado en data para manipularlo
        console.log(res.data)               //cómo me traeré pages de info?
      })                                    //elsint+prettier
      .catch(err => console.log(err));
    },
    seemore (id){
      this.$router.push(`char/${id}`)
    },
  },
  created() {
    this.fetch(this.pageSelect);
    console.log('created called')
  },
  watch: {
    pageSelect: function (value){
      this.fetch(value)
    }
  }
};
</script>
<style>
.flex{
  padding: 2%
}
* {
  /*padding: 4px;*/
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
