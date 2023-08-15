<script>
export default {
  props: {
    characters: {
      type: Array,
      required: true
    }
  },
  computed: {
    totalAgeOfGroup() {
      let xSum = 0

      for (let obj of this.characters) {
        for (let key in obj) {
          if (key === 'age') {
            xSum += obj[key]
          }
        }
      }

      console.log(xSum) // 9
      return xSum
    },
    getRelationshipCount() {
      const statusCount = {}

      this.characters.forEach((character) => {
        if (statusCount[character.relationship]) {
          statusCount[character.relationship]++
        } else {
          statusCount[character.relationship] = 1
        }
      })

      return statusCount
    }
  }
}
</script>

<template>
  <h2>Statistics</h2>
  <ul>
    <li v-for="[index, value] in Object.entries(getRelationshipCount)" :key="`${index}`">
      {{ index }}:
      {{ value }}
    </li>
  </ul>
  <div class="stats">
    The total age of the F.R.I.E.N.D.S Group: <mark>{{ totalAgeOfGroup }}</mark>
  </div>
</template>
