<script>
import axios from "axios";
export default {
  name: "nasaApi",
  GetNasaPictureOfTheDay() {
    return axios.get(
      "https://api.nasa.gov/planetary/apod?api_key=r6oklW46NQbS9iU3uJNJZOfxrTifEAwHks4XBLoc"
    );
  },
  getNasaData(dateYYYMMdd) {
    return axios.get(
      `https://api.nasa.gov/planetary/apod?api_key=r6oklW46NQbS9iU3uJNJZOfxrTifEAwHks4XBLoc&date=${dateYYYMMdd}`
    );
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
