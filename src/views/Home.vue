<template>
  <character />
</template>

<script>
import character from '../components/character';
import axios from 'axios'

export default {
  components: {
    character,
  },
  methods: {
    showModal (id){
      this.fetchOne(id)
    },
    async fetchOne (id){
      let result = await axios.get(`https://rickandmortyapi.com/api/character/${id}/`);
      this.currentCharacter = result.data;
      this.modal = true;

      console.log(this.currentCharacter, "personaje")
    },
    watchMore (id){
      this.$emit('showModal',id)
    }
  }
};
</script>
