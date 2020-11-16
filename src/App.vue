<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <!-- send the request api -->
    <button v-on:click.prevent="sendApiRequest">Search</button>
    <!-- show a loading img while we wait for the info -->
    <!-- v-if create a bolean statement  true or false-->
    <img v-if="loading" :src="gif" />
    <section class="images">
      <img :src="images.message" />
    </section>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      gif:
        "https://cdn.dribbble.com/users/2077073/screenshots/7103423/media/223825c7f91575b639fd71f3accff8f4.gif",
      title: "Search Random Dog",
      images: [],
      // set the loading state to true. this mean the gif will run ulti the user click the btn search
      loading: true,
    };
  },
  methods: {
    async sendApiRequest() {
      //while we get the data from the api show the gif
      this.loading = true;
      // clear the previous data sent by the request
      this.images = [];
      // eslint-disable-next-line no-unused-vars
      const response = await fetch(`https://dog.ceo/api/breeds/image/random`)
        //converter the response to json format
        .then((data) => data.json());
      console.log(response);
      //store the data into the state array images
      this.images = response;
      console.log(this.images);
      //when the data is loaded the gift disapear
      this.loading = false;
    },
  },
};
</script>

<style>
#app {
  text-align: center;
}
body {
  width: 80%;
  margin: 2em auto 0 auto;
}
.images {
  margin: 0 auto;
  width: 100%;
}

img {
  width: 100%;
  max-height: 700px;
}
</style>
