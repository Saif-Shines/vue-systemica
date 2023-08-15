<script>
import FriendsStats from '@/components/FriendsStats.vue'
import CharacterCard from '@/components/CharacterCard.vue'
import AddNewCharacterCard from './components/AddNewCharacter.vue'

export default {
  components: {
    FriendsStats,
    CharacterCard,
    AddNewCharacterCard
  },
  data() {
    return {
      title: 'Who are the characters in the show?',
      characterList: [
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
      favoriteCharacters: []
    }
  },
  methods: {
    addtoFavList(payload) {
      console.log('value', payload)
      this.favoriteCharacters.push(payload)
      console.log(this.favoriteCharacters)
    },
    addToCharacterList(newCharacter) {
      console.log('newCharacter', newCharacter)
      let capitalizedName = this.capitalizeFirstWord(newCharacter)
      this.characterList.push({ name: capitalizedName, relationship: 'unknown' })
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
  <h1>{{ title }}</h1>
  <FriendsStats :characters="characterList" />
  <hr />
  <aside>
    <h3>Favorite Characters</h3>
    <i>List of Fav characters will appear</i>
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
    placeholder="Guess?"
    aria-label="character box"
    v-model="answer"
  />
  <hr />
  <div v-if="answer == ''">❗Type your answer</div>
  <div v-else-if="characterList.some((actor) => actor.name == answer.toLowerCase())">
    {{ right }}
  </div>
  <div v-else>
    {{ wrong }}
    <hr />
    <CharacterCard
      :capitalize="capitalizeFirstWord"
      :character="characterList"
      @favorite="addtoFavList"
    />
  </div>
  <AddNewCharacterCard @addCharacter="addToCharacterList" />
</template>
