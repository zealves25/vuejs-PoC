<script>
export default {
  data: () => ({
    newCharacter: {
      name: "",
      element: [],
    },
    characters: [
      { name: "Gandalf", elements: ["Air", "Earth", "Water", "Fire"] },
      { name: "Aragorn", elements: ["Air", "Fire"] },
      { name: "Legolas", elements: ["Grass"] },
      { name: "Frodo", elements: ["Water", "Earth"] },
    ],
    favoriteCharacters: [],
  }),
  methods: {
    favoriteCharacter(character) {
      this.favoriteCharacters.push(character);
    },
    addNewCharacter() {
      this.characters.push(this.newCharacter);
      this.newCharacter = { name: "" };
    },
  },
  computed: {
    benderStatistics() {
      const allElements = ["Air", "Fire", "Water", "Grass", "Earth"];

      const statistics = {
        Air: 0,
        Water: 0,
        Fire: 0,
        Earth: 0,
        Grass: 0,
      };

      this.characters.forEach((character) => {
        allElements.forEach((element) => {
          if (character.elements.indexOf(element) > -1) {
            statistics[element] += 1;
          }
        });
      });

      return statistics;
    },
  },
};
</script>

<template>
  <h2>Statistics</h2>
  <ul>
    <li v-for="(stat, type) in benderStatistics" :key="`stat-${type}`">
      {{ type }}: {{ stat }}
    </li>
  </ul>
  <h2>Characters</h2>
  <ul>
    <li v-for="(character, index) in characters" :key="`character-${index}`">
      <p>{{ character.name }}</p>
      <button @click="favoriteCharacter(character)">favorite</button>
    </li>
  </ul>
  <h2>Favorite Characters</h2>
  <ul v-if="favoriteCharacters.length > 0">
    <li
      v-for="(character, index) in favoriteCharacters"
      :key="`favorite-character-${index}`"
    >
      {{ character.name }}
    </li>
  </ul>
  <p v-else>There are no favorites</p>
  <h2>New character</h2>
  <pre>{{ newCharacter }}</pre>
  <label for="name">Name</label>
  <input
    type="text"
    v-model="newCharacter.name"
    @keyup.enter="addNewCharacter"
  />
</template>
