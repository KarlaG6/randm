<template>
  <v-layout justify-center wrap>
  <v-flex xs12 sm6>
    <v-card>
      <v-card-title class="grey darken-1">
        <span class="headline white--text">{{ currentCharacter.name }}</span>
        <v-spacer></v-spacer>
        <span class="headline white--text">{{ currentCharacter.id }}</span>
        
      </v-card-title>

      <v-list>
        <v-list-item>
          <v-list-item-action>
            <v-icon>mdi-map-marker</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>{{ currentCharacter.location.name }}</v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>

          </v-list-item-action>
        </v-list-item>

        <v-divider inset></v-divider>

        <v-list-item>
          <v-list-item-action>
            <v-icon>mdi-gender-{{currentCharacter.gender.toLowerCase() }}</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>{{ currentCharacter.gender}}</v-list-item-title>
          </v-list-item-content>

        </v-list-item>

        <v-divider inset></v-divider>

        <v-list-item >
          <v-list-item-action>
            <v-icon>mdi-baby-face-outline</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>{{currentCharacter.origin.name}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-divider inset></v-divider>

        <v-list-item >
          <v-list-item-action>
            <v-icon>mdi-skull</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>{{currentCharacter.status}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
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
      currentCharacter: {}
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
  margin-top: 8%;
}
div#app{
  background-color: black 
}
</style>

