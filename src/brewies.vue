<template>
  <div class="brews">
    <h2>Brew Search</h2>
    <section>
      <button @click.prevent="submitted">Submit</button>
    </section>
    <div class="search-results" v-for="brewery in breweries" :key="brewery.id">
      <ul>
        <li>
          <span class="title">Name:</span>
          <span class="brew">{{ brewery.name }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      breweries: [],
    };
  },
  methods: {
    async submitted() {
      console.log();
      const response = await fetch(
        `https://api.openbrewerydb.org/breweries/?by_name=pub`
      ).then((res) => res.json());
      console.log(response);
      this.breweries = response;
    },
  },
};
</script>

<style scoped>
.search-results {
  display: flex;
  width: 600px;
  text-align: left;
}
.brews {
  max-width: 1024px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 0 auto;
}
ul {
  list-style-type: none;
  width: 100%;
}
li {
  display: flex;
  justify-content: space-between;
}
.brew {
  font-weight: bold;
}
</style>
