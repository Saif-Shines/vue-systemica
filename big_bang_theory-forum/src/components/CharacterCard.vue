<script>
export default {
  props: {
    capitalize: {
      type: Function,
      required: true
    },
    character: {
      type: Object,
      required: true
    }
  },
  emits: ['favorite'],
  methods: {
    favoriteCharacter(actor) {
      this.$emit('favorite', actor)
    }
  }
}
</script>

<template>
  <div>
    <h2>Select a Favorite Character:</h2>
    <ul>
      <li v-for="(actor, index) in character" :key="`${index}`">
        {{ capitalize(actor.name) }}
        <button class="favorite-btn" @click="favoriteCharacter(actor)">Mark Favorite</button>
      </li>
    </ul>
  </div>
</template>
