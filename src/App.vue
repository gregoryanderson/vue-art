<template>
  <div id="app">
    <h1>Pictures</h1>
    <button v-if="this.prev" @click="getPrevPictures()">Previous</button>
    <button @click="getNextPictures()">Next</button>
    <pictures :pictures="pictures" />
  </div>
</template>

<script>
import Pictures from "@/components/Pictures.vue";

export default {
  name: "app",
  components: {
    Pictures
  },
  data() {
    return {
      pictures: [],
      error: "",
      next: "",
      prev: ""
    };
  },
  mounted() {
    this.getPictures();
  },
  methods: {
    async getPictures() {
      try {
        const response = await fetch(
          `https://api.harvardartmuseums.org/object?classification=Prints&q=totalpageviews:1&apikey=${process.env.VUE_APP_APIKEY}`
        );
        const data = await response.json();
        this.cleanData(data);
      } catch (error) {
        this.error = { error };
      }
    },
    async getNextPictures() {
      try {
        const url = this.next;
        const response = await fetch(url);
        const data = await response.json();
        this.cleanData(data);
      } catch (error) {
        this.error = { error };
      }
    },
    async getPrevPictures() {
      try {
        const url = this.next;
        const response = await fetch(url);
        const data = await response.json();
        this.cleanData(data);
      } catch (error) {
        this.error = { error };
      }
    },
    cleanData(data) {
      this.next = data.info.next;
      this.prev = data.info.prev;
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
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

html {
  background-color: black;
  color: white;
}

h1 {
  background-color: black;
  color: white;
  margin: 0;
  padding: 100px;
}
</style>
