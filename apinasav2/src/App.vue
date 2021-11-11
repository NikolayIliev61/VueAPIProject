<template>
  <section>
    <div class="wrapper" v-if="info">
      <div class="date">
        <h1>{{ info.date }}</h1>
      </div>
      <div class="title">
        <h2>{{ info.title }}</h2>
      </div>
      <div class="picture">
        <img :src="this.info.url" alt="Picture of the day" />
      </div>
      <div><button class="btn" @click="toggleShow">See More</button></div>
      <div class="details" v-show="show">
        <p>{{ info.explanation }}</p>
        <p>{{ info.copyright }}</p>
      </div>
    </div>
    <DatePicker></DatePicker>
  </section>
</template>

<script>
import nasaApi from "./components/nasaApi.vue";
import DatePicker from "./components/DatePicker.vue";
export default {
  name: "App",
  components: {
    DatePicker,
  },
  data() {
    return {
      info: "",
      show: false,
    };
  },
  methods: {
    toggleShow() {
      this.show = !this.show;
    },
  },
  created() {
    nasaApi.GetNasaPictureOfTheDay().then((response) => {
      console.log(response.data);
      this.info = response.data;
    });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
body {
  background-color: black;
}
.picture img {
  width: 700px;
}
.btn {
  margin-top: 60px;
  margin-bottom: 30px;
  cursor: pointer;
  width: 130px;
  padding: 10px;
  border: 2px solid black;
  border-radius: 7px;
  background-color: rgb(170, 223, 85);
}
.btn:hover {
  background-color: rgb(rgb(182, 112, 112), green, blue);
}

.details p {
  width: 800px;
  letter-spacing: 0.1em;
  margin: 0 auto;
  margin-bottom: 20px;
}
</style>
