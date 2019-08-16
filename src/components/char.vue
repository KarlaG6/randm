<template>
  <v-layout justify-center wrap>
  <v-flex xs12 sm8>
    <v-card>
      <v-card-title class="grey darken-1">
        <span class="headline white--text">{{ currentCharacter.name }}</span>
        <v-spacer></v-spacer>
        <span class="headline white--text">{{ currentCharacter.id }}</span>
        
      </v-card-title>
      <v-list v-for="item in items" :key="item.name" :items="items">
        <v-list-item>
          <v-list-item-action>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title v-text="item.itemTitle" :itemTitle="itemTitle"></v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>

          </v-list-item-action>
        </v-list-item>

        <v-divider inset></v-divider>
         </v-list>
        
      <v-img  :src="currentCharacter.image"  height="200px"></v-img>
    </v-card>
  </v-flex>
</v-layout>
</template>
<script>
import axios from 'axios'
export default {
  props: ['id'],
  data: () => ({
      currentCharacter: {},
      items:[
        {icon:'mdi-map-marker',itemTitle:'currentCharacter.location.name',name:"location"},
        {icon:'mdi-gender-${currentCharacter.gender.toLowerCase() }',itemTitle:'currentCharacter.gender',name:"gender"},
        {icon:'mail',itemTitle:'currentCharacter.origin.name',name:"origin"},
        {icon:'mdi-skull',itemTitle:'currentCharacter.status',name:"status"}
      ]
  }),
  created () {
    this.fetchOne()
  },
  methods:{
    async fetchOne (){
      let { data } = await axios.get(`https://rickandmortyapi.com/api/character/${this.id}/`);
      this.currentCharacter = data;
      console.log(this.currentCharacter)
    }
  }
}
</script>
<style>
.v-card.v-sheet.theme--light{
  margin-top: 8%
}
div#app{
  background-color: black 
}
</style>

