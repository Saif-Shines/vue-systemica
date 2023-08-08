<script>
export default {
  data() {
    return {
      title: 'Who are the characters in the show?',
      characters: [
        {
          name: 'penny',
          age: 26,
          area: 'US',
          relationship: 'committed'
        },
        {
          name: 'sheldon',
          age: 27,
          area: 'Texas',
          relationship: 'searching'
        },
        {
          name: 'leonard',
          age: 26,
          area: '',
          relationship: 'single'
        },
        {
          name: 'raj',
          age: 25,
          area: 'Mumbai',
          relationship: 'single'
        },
        {
          name: 'bernadette',
          age: 28,
          area: 'Canada',
          relationship: 'single'
        },
        {
          name: 'amy',
          age: 30,
          area: 'Asian',
          relationship: 'committed'
        }
      ],
      right: '✔️ You are absolutely correct!',
      wrong: '⚠️ Oops! You did not watch The Big Bang Theory Properly!',
      answer: '',
      newCharacter: '',
      favoriteCharacters: []
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
  },
  methods: {
    addtoFavList(value) {
      console.log('value', value)
      this.favoriteCharacters.push(value)
      console.log(this.favoriteCharacters)
    },
    addToCharacterList(newCharacter) {
      console.log('newCharacter', newCharacter)
      let capitalizedName = this.capitalizeFirstWord(newCharacter)
      this.characters.push({ name: capitalizedName })
      console.info('all characters now', this.characters)
    },
    capitalizeFirstWord(string) {
      const words = string.split(' ')
      words[0] = words[0].charAt(0).toUpperCase() + words[0].slice(1)
      return words.join(' ')
    }
  }
}
</script>

<template>
  <h2>{{ title }}</h2>
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
  <aside>
    <h3>Favorite Characters</h3>
    <ol>
      <li v-for="(fav, index) in favoriteCharacters" :key="`${index}`">
        {{ capitalizeFirstWord(fav.name) }}
      </li>
    </ol>
  </aside>
  <input
    type="text"
    size="30"
    maxlength="30"
    placeholder="Character"
    aria-label="character box"
    v-model="answer"
  />
  <br />
  <div v-if="answer == ''">❗Type your answer</div>
  <div v-else-if="characters.some((actor) => actor.name == answer.toLowerCase())">
    {{ right }}
    <label for="addCharacter">Did we miss an character? Add it!</label>
    <input type="text" id="addCharacter" v-model="newCharacter" />
    <button @click="addToCharacterList(newCharacter)" class="favorite-btn">Add</button>
  </div>
  <div v-else>
    {{ wrong }}
    <hr />
    <ul>
      <li v-for="(actor, index) in characters" :key="`${index}`">
        {{ capitalizeFirstWord(actor.name) }}
        <button class="favorite-btn" @click="addtoFavList(actor)">Mark Favorite</button>
      </li>
    </ul>
  </div>
</template>
