<script>
export default {
  data() {
    return {
      newCharacter: ''
    }
  },
  emits: ['addCharacter'],
  methods: {
    addAnCharacter(charName) {
      this.$emit('addCharacter', charName)
    }
  }
}
</script>

<template>
  <h3>Did we miss an character?</h3>
  <label for="addCharacter"> Add it!</label>
  <input type="text" id="addCharacter" v-model="newCharacter" />
  <button @click="addAnCharacter(newCharacter)" class="favorite-btn">Add</button>
</template>

<style>
button {
  background-color: #e9e9e9;
  box-sizing: border-box;
  border: none;
  color: #4a6db3;
  padding: 1px 10px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
  border-radius: 4px;
}
</style>
