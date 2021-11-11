<script setup>
import Datepicker from "vue3-datepicker";
import nasaApi from "./nasaApi.vue";
import { ref } from "vue";
const picked = ref(new Date());
let message =
  "There is a bug! Please click twice on the same date in order to work. Soon it will be fixed.";
function formatDate(date) {
  const offset = date.getTimezoneOffset();
  date = new Date(date.getTime() - offset * 60 * 1000);
  return date.toISOString().split("T")[0];
}

function getNasaDataKuraMi() {
  var formattedDate = formatDate(picked.value);
  nasaApi
    .getNasaData(formattedDate)
    .then((response) => {
      console.log(response.data);
      this.results = response.data;
    })
    .catch((error) => {
      console.log(error);
    });
}
</script>

<template>
  <section>
    <section class="datepicker">
      <datepicker v-model="picked" v-on="getNasaDataKuraMi()" />

      <div class="message">{{ message }}</div>
    </section>
    <section>
      <div class="wrapper" v-if="results">
        <div class="date">
          <h1>{{ results.date }}</h1>
        </div>
        <div class="title">
          <h2>{{ results.title }}</h2>
        </div>
        <div class="picture">
          <img :src="this.results.url" alt="Picture of the day" />
        </div>
        <div class="details">
          <p>{{ results.explanation }}</p>
          <p>{{ results.copyright }}</p>
        </div>
      </div>
    </section>
  </section>
</template>
<style scoped>
.message {
  margin-top: 30px;
}
.picture img {
  margin-bottom: 30px;
}
</style>
