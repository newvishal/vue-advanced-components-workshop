<template>
  <div>
    <hero
      v-for="hero in heroes"
      :key="hero.id"
      :data="hero"
      @select="selectHero"
    />
    <div>{{ selectedHeroes }}</div>
    <button @click="randomSelect">Select random heroes</button>
  </div>
</template>

<script>
import Hero from './Hero.vue';

export default {
  name: 'hero-list',
  components: {
    Hero,
  },
  data() {
    return {
      heroes: [
        {
          id: 1,
          firstName: 'Bogdan',
          lastName: 'Luca',
          framework: 'Vue',
          selected: false,
        },
        {
          id: 2,
          firstName: 'Andrei',
          lastName: 'Antal',
          framework: 'Angular',
          selected: false,
        },
        {
          id: 3,
          firstName: 'Sabin',
          lastName: 'Marcu',
          framework: 'React',
          selected: false,
        },
      ],
    };
  },
  computed: {
    selectedHeroes() {
      const names = this.heroes
        .filter(hero => hero.selected)
        .map(hero => hero.firstName);
      return names.length
        ? `Selected heroes: ${names.join(', ')}`
        : 'No selected heroes';
    },
  },
  methods: {
    randomSelect() {
      for (const hero of this.heroes) {
        hero.selected = Math.random() < 0.5;
      }
    },
    selectHero({ id, value }) {
      const heroIndex = this.heroes.findIndex(h => h.id === id);
      this.heroes[heroIndex].selected = value;
    },
  },
};
</script>

<style scoped>
button {
  margin-top: 10px;
}
</style>
