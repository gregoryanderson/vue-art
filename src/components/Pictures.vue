<template>
  <div class="pictures">
    <div :key="picture.id" v-for="picture in pictures" class="frame">
      <div class="info">
        <h2>{{picture.title}}</h2>
        <div class="info-small">
          <p>{{picture.artist}}</p>
          <p>{{picture.date}}</p>
          <p>{{picture.culture}}</p>
          <p>{{picture.technique}}</p>
        </div>
      </div>
      <li class="inlay">
        <img :src="picture.url" width="600px" />
      </li>
    </div>
  </div>
</template>

<script>
export default {
  name: "Pictures",
  props: {
    pictures: [],
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li {
  display: inline-block;
}

.info {
  justify-content: space-between;
  margin: 0px 100px;
}

.info-small {
    width: 95%;
    display: flex; 
    justify-content: space-between;
    margin: auto;
    color: white;
}


.frame {
  box-sizing: border-box;
  position: relative;
  background: black;
  padding: 7px;
}

.inlay {
  box-shadow: inset -1px 1px 6px 1px rgba(0, 0, 0, 0.24);
  background: whitesmoke;
  align-items: center;
  padding: 75px;
  margin-bottom: 100px;
}

p {
  margin: 0;
}

img {
  border: 1px solid black;
}

h2 {
  margin: 0;
  font-size: 50px;
  color: white;
}
</style>
