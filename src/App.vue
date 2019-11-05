<template>
  <div id="app">
    <h1>Pictures</h1>
  </div>
</template>

<script>

export default {
  name: "app",
  components: {

  },
  data() {
    return {
      pictures: [],
      error: ""
    };
  },
  mounted() {
    this.getPictures();
  },
  methods: {
    async getPictures() {
      try {
        const response = await fetch(
          "https://api.harvardartmuseums.org/object?classification=Prints&q=totalpageviews:1&apikey=a9cbeb10-fe90-11e9-b607-3f3e8e4ed76b"
        );
        const data = await response.json();
        this.cleanData(data);
      } catch (error) {
        this.error = { error };
      }
    },
    cleanData(data) {
      this.pictures = data.records.map(picture => {
        return {
          artist: picture.people[0].alphasort,
          url: picture.primaryimageurl,
          id: picture.id,
          date: picture.dated,
          culture: picture.culture,
          title: picture.title,
          technique: picture.technique
        };
      });
    }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
